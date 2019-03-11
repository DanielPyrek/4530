```python

from aguaclara.core.units import unit_registry as u
import aguaclara.research.environmental_processes_analysis as epa
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats
import collections
import os
from pathlib import Path

# This code is included because there is a bug in the version of this code that is in epa.

def aeration_data(DO_column, dirpath):
    """This function extracts the data from folder containing tab delimited
    files of aeration data. The file must be the original tab delimited file.
    All text strings below the header must be removed from these files.
    The file names must be the air flow rates with units of micromoles/s.
    An example file name would be "300.xls" where 300 is the flowr ate in
    micromoles/s. The function opens a file dialog for the user to select
    the directory containing the data.

    Parameters
    ----------
    DO_column : int
        index of the column that contains the dissolved oxygen concentration
        data.

    dirpath : string
        path to the directory containing aeration data you want to analyze

    Returns
    -------
    filepaths : string list
        all file paths in the directory sorted by flow rate

    airflows : numpy array
        sorted array of air flow rates with units of micromole/s attached

    DO_data : numpy array list
        sorted list of numpy arrays. Thus each of the numpy data arrays can
        have different lengths to accommodate short and long experiments

    time_data : numpy array list
        sorted list of numpy arrays containing the times with units of seconds

    Examples
    --------

    """
    #return the list of files in the directory
    filenames = os.listdir(dirpath)
    #extract the flowrates from the filenames and apply units
    airflows = ((np.array([i.split('.', 1)[0] for i in filenames])).astype(np.float32))
    #sort airflows and filenames so that they are in ascending order of flow rates
    idx = np.argsort(airflows)
    airflows = (np.array(airflows)[idx])*u.umole/u.s
    filenames = np.array(filenames)[idx]

    filepaths = [os.path.join(dirpath, i) for i in filenames]
    #DO_data is a list of numpy arrays. Thus each of the numpy data arrays can have different lengths to accommodate short and long experiments
    # cycle through all of the files and extract the column of data with oxygen concentrations and the times
    DO_data=[epa.column_of_data(i,0,DO_column,-1,'mg/L') for i in filepaths]
    time_data=[(epa.column_of_time(i,0,-1)).to(u.s) for i in filepaths]
    aeration_collection = collections.namedtuple('aeration_results','filepaths airflows DO_data time_data')
    aeration_results = aeration_collection(filepaths, airflows, DO_data, time_data)
    return aeration_results



# The column of data containing the dissolved oxygen concentrations
DO_column = 2
acc_column = 1
dirpath = "data/Aeration/"
filepaths, airflows, DO_data, time_data = aeration_data(DO_column,dirpath)
Accumulator = []

# Plot the raw data
DO_min = 2 * u.mg/u.L
DO_max = 6 * u.mg/u.L
for i in range(airflows.size):
  idx_start = (np.abs(DO_data[i]-DO_min)).argmin()
  idx_end = (np.abs(DO_data[i]-DO_max)).argmin()
  time_data[i] = time_data[i][idx_start:idx_end] - time_data[i][idx_start]
  DO_data[i] = DO_data[i][idx_start:idx_end]


for i in range(airflows.size):
  plt.plot(time_data[i], DO_data[i],'-')
plt.xlabel(r'$time (s)$')
plt.ylabel(r'Oxygen concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(airflows.magnitude)
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer')
plt.show()



for i in 2,3,6,8,9,:
  plt.plot(time_data[i], DO_data[i],'-')
plt.xlabel(r'$time (s)$')
plt.ylabel(r'Oxygen concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(airflows.magnitude)
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer2')
plt.show()

P_air = 1*u.atmosphere
temp = 298*u.kelvin

C_star = (epa.O2_sat(P_air,temp))*(u.L/u.mg)
C_star

time_data
kvalues = ()
for i in range (0,23):
  DOdata = DO_data[i]
  timedata = time_data[i]
  x = ()
  y = ()
  DOo = DOdata[0]*(u.L/u.mg)
  DOo
  for k in range (0,timedata.size-1):
    ew = np.absolute((C_star - DOdata[k]*(u.L/u.mg))/(C_star -  DOo))
    y = np.append(y,ew)
    x = np.append(x,timedata[k]/(u.second))


  stats.linregress(x, y)
  slope, intercept, r_value, p_value, std_err = stats.linregress(x,y)
  kvalues = np.append(kvalues,slope)


kvalues = -kvalues

test = 0

t = np.array(range(200))*u.dimensionless
DOdata = DO_data[test]*(u.L/u.mg)
k = kvalues[test]*u.dimensionless
C = -(C_star-DOdata[0])*2.71828**((-k*t).to(u.dimensionless).magnitude)+C_star

timedata = time_data[test]
DOdata = DO_data[test]
#C=-k.to(u.dimensionless).magnitude*t.to(u.dimensionless).magnitude+DOdata[7]

plt.plot(t,C,'g')
plt.plot(timedata,DOdata,'ro')



xx = (100,125,175,200,225,250,350,400,450,475,500,525,575,650,700,725,750,775,800,825,850,925,950)
plt.plot(xx,kvalues,'o')



#delete data that is less than 2 or greater than 6 mg/L


```
C^{\star} =P_{O_{2}} {\mathop{e}\nolimits^{\left(\frac{1727}{T} -2.105\right)}}


$$ C = - (C^{*} - C_o)*e^{-kt} +  C^{*}  $$
