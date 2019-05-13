````python

from aguaclara.core.units import unit_registry as u
import aguaclara.research.environmental_processes_analysis as epa
import aguaclara.core.physchem as pc
import aguaclara.core.utility as ut
import numpy as np
import matplotlib.pyplot as plt
import collections
import os
from pathlib import Path
import pandas as pd



def adsorption_data(C_column, dirpath):
    """This function extracts the data from folder containing tab delimited
    files of adsorption data. The file must be the original tab delimited file.

    Parameters
    ----------
    C_column : int
        index of the column that contains the dissolved oxygen concentration
        data.
    dirpath : string
        path to the directory containing aeration data you want to analyze
    Returns
    -------
    filepaths : string list
        all file paths in the directory sorted by flow rate
    time_data : numpy array list
        sorted list of numpy arrays containing the times with units of seconds
    Examples
    --------
    """
    #return the list of files in the directory
    metadata = pd.read_csv(dirpath + '/metadata.txt', delimiter='\t')
    filenames = metadata['file name']
    #extract the flowrates from the filenames and apply units
    #sort airflows and filenames so that they are in ascending order of flow rates


    filepaths = [dirpath + '/' + i for i in filenames]
    #C_data is a list of numpy arrays. Thus each of the numpy data arrays can have different lengths to accommodate short and long experiments
    # cycle through all of the files and extract the column of data with oxygen concentrations and the times
    C_data=[epa.column_of_data(i, 2,-1) for i in filepaths]
    time_data=[(epa.column_of_time(i,2,-1)).to(u.s) for i in filepaths]

    adsorption_collection = collections.namedtuple('adsorption_results','metadata filenames C_data time_data')
    adsorption_results = adsorption_collection(metadata, filenames, C_data, time_data)
    return adsorption_results

for y in range (0 to 3):
  for z in range (0 to size(C_data[y]))
  C_data[y][z] =   C_data[y][z]*u.mg/u.liter


C_column = 1
dirpath = "https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Final/"


metadata, filenames, C_data, time_data = adsorption_data(C_column,dirpath)
metadata

Column_D = 1 * u.inch
Column_A = pc.area_circle(Column_D)
Column_L = 15.2 * u.cm
Column_V = Column_A * Column_L
#I'm guessing at the volume of water in the tubing, in the photometer, and in the space above and below the column. This parameter could be adjusted!
Tubing_V = 60 * u.mL
Flow_rate = ([metadata['flow (mL/s)'][i] for i in metadata.index])* u.mL/u.s
Mass_carbon= ([metadata['carbon (g)'][i] for i in metadata.index])* u.g
Tubing_HRT = Tubing_V/Flow_rate
#to make things simple we are assuming that the porosity is the same for sand and for activated carbon. That is likely not true!
porosity = 0.4
C_0 = 50 * u.mg/u.L

#estimate the HRT for all of the columns
HRT = (porosity * Column_V/Flow_rate).to(u.s)

#zero the concentration data by subtracting the value of the first data point from all data points. Do this in each data set.

L_column = 15.2 * u.cm
D_column = 1*u.inch
A_column = pc.area_circle(D_column)
V_column = (A_column * L_column).to(u.mL)


for i in range(np.size(filenames)):
  C_data[i]=C_data[i]-C_data[i][0]

svals50y = ()
svals50x = ()
sTwater = ()
#Create a graph of the columns that didn't have any activated carbon
mylegend = []
for i in range(np.size(filenames)):
  if (metadata['carbon (g)'][i] == 0):
    plt.plot(time_data[i]/HRT[i] - Tubing_HRT[i]/HRT[i], C_data[i]/C_0,'-');
    mylegend.append(str(metadata['flow (mL/s)'][i]) + ' mL/s')
    for k in range(np.size(C_data[i])):
        if float(C_data[i][k]/C_0) >= 0.5:
            T = (time_data[i][k]-time_data[i][k-1])/(C_data[i][k]/C_0-C_data[i][k-1]/C_0)*(0.5-C_data[i][k-1]/C_0)+time_data[i][k-1]
            svals50y = np.append(svals50y,T)
            svals50x = np.append(svals50x,metadata['carbon (g)'][i])
            timewater = V_column/(metadata['flow (mL/s)'][i])
            sTwater= np.append(sTwater,timewater)
            break


plt.xlabel(r'$\frac{t}{\theta}$');
plt.xlim(right=3,left=0);
plt.ylabel(r'Red dye concentration $\left ( \frac{mg}{L} \right )$');
plt.legend(mylegend);
plt.savefig('C:/Users/dapmo/github/4530/Final/Test')
plt.show()

# R_adsorption
sR_adsorption = svals50y/sTwater
sR_adsorption





vals50y =()
vals50x =()
Twater = ()
# create a graph of the columns that had different masses of activated carbon. Note that this includes systems with different flow rates!
mylegend =[]
for i in range(np.size(filenames)):
  if (metadata['carbon (g)'][i] != 0):
    plt.plot(time_data[i]/HRT[i] - Tubing_HRT[i]/HRT[i], C_data[i]/C_0,'-');
    mylegend.append(str(ut.round_sf(metadata['carbon (g)'][i],3)) + ' g, ' + str(ut.round_sf(metadata['flow (mL/s)'][i],2)) + ' mL/s')
    for k in range(np.size(C_data[i])):
        if C_data[i][k]/C_0 >= 0.5:
          T = (time_data[i][k]-time_data[i][k-1])/(C_data[i][k]/C_0-C_data[i][k-1]/C_0)*(0.5-C_data[i][k-1]/C_0)+time_data[i][k-1]
          vals50y = np.append(vals50y,T)
          vals50x = np.append(vals50x,metadata['carbon (g)'][i])
          timewater = V_column/(metadata['flow (mL/s)'][i])
          Twater= np.append(Twater,timewater)
          break

plt.xlabel(r'$\frac{t}{\theta}$');
plt.xlim(right=30,left=0);
plt.ylabel(r'Red dye concentration $\left ( \frac{mg}{L} \right )$');
plt.legend(mylegend);
plt.savefig('C:/Users/dapmo/github/4530/Final/Test2')

plt.show()


plt.xlabel(r'Mass of Activated Carbon (g)');
plt.ylabel(r'time when the effluent concentration was 50% (s)');
plt.legend(mylegend);

plt.plot(vals50x,vals50y, 'ro')
plt.savefig('C:/Users/dapmo/github/4530/Adsorptiontimeto50')
plt.show()

# Carbon R_adsorption
R_adsorption = vals50y/Twater
R_adsorption

vals50y/vals50x


qo = (R_adsorption-1)*(C_0*porosity*V_column/vals50x)/1000000
qo

plt.xlabel(r'Mass of Activated Carbon (g)');
plt.ylabel(r'qo');
plt.legend(mylegend);

plt.plot(vals50x,qo, 'bo')
plt.savefig('C:/Users/dapmo/github/4530/Final/Test3')
plt.show()




plt.xlabel(r'$\frac{t}{\theta}$');
plt.xlim(right=100,left=0);
plt.ylabel(r'Red dye concentration $\left ( \frac{mg}{L} \right )$');
plt.legend(mylegend);
plt.savefig('C:/Users/dapmo/github/4530/Final/Test4')
plt.show()
```
