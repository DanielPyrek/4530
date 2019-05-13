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



C_column = 1
dirpath = "https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Final/"


metadata, filenames, C_data, time_data = adsorption_data(C_column,dirpath)
metadata


#zero the concentration data by subtracting the value of the first data point from all data points. Do this in each data set.

for k in range(np.size(filenames)):
  test = 1000
  for z in range(np.size(time_data[k])):
    if (C_data[k][z] < test and C_data[k][z] > 0):
      test = C_data[k][z]
  for y in range(np.size(time_data[k])):
    C_data[k][y] = C_data[k][y] - test



#PLOT ALL ON SAME PLOT


i =0
plt.plot(time_data[i], C_data[i],'-',label = "Activated Carbon");
i =1
plt.plot(time_data[i], C_data[i],'-',label = "Charcoal");
i =2
plt.plot(time_data[i], C_data[i],'-', label = "Salted Treated Charcoal");
i =3
plt.plot(time_data[i], C_data[i],'-', label = "Sand");
plt.xlim([0,40000])
plt.ylim([0,27])


plt.xlabel(r'Time (s)');
plt.ylabel(r'Red dye concentration $\left ( \frac{mg}{L} \right )$');
plt.legend()
plt.title('All Tests')
plt.savefig('C:/Users/dapmo/github/4530/data/Final/FINALAll')
plt.show()

#PLOT CARBON

i =0
plt.plot(time_data[i], C_data[i],'-',label = "Activated Carbon");
plt.xlim([0,43000])
plt.ylim([0,27])

plt.axhline(y=25, color='r', linestyle='-', label = "Half of Influent Red Dye Concentration")

plt.xlabel(r'Time (s)');
plt.ylabel(r'Red dye concentration $\left ( \frac{mg}{L} \right )$');
plt.legend()
plt.title('Activated Carbon')
plt.savefig('C:/Users/dapmo/github/4530/data/Final/FINAL1')
plt.show()


#PLOT ALL OTHERS

i =1
plt.plot(time_data[i], C_data[i],'-',label = "Charcoal");
i =2
plt.plot(time_data[i], C_data[i],'-', label = "Salted Treated Charcoal");
i =3
plt.plot(time_data[i], C_data[i],'-', label = "Sand");

plt.axhline(y=25, color='r', linestyle='-')

plt.title('Charcoal, Salt Treated Charcoal, and Sand')
plt.xlabel('Time (s)');
plt.xlim(0,800);
plt.ylabel(r'Red dye concentration $\left ( \frac{mg}{L} \right )$');
plt.legend();
plt.savefig('C:/Users/dapmo/github/4530/data/Final/FINAL3')
plt.show()


#FIND BREAKTHROUGH POINTS
breakthrough = ();
for k in range(np.size(filenames)):
  for z in range(np.size(time_data[k])):
    if (C_data[k][z] > 1 and time_data[k][z] > 50*u.second):
      breakthrough = np.append(breakthrough,time_data[k][z]);
      break

print(breakthrough)
breakthrough = np.asarray(breakthrough)

#Amount of water treated before breakthroughs
mLperRev = (2.8*(u.mL)/(u.revolution)).to((u.liter)/(u.revolution))
Q = (10*u.revolution/u.minute).to(u.revolution/u.second)
watertreated = [Q*mLperRev*breakthrough[0]*u.second,Q*mLperRev*breakthrough[1]*u.second,Q*mLperRev*breakthrough[2]*u.second,Q*mLperRev*breakthrough[3]*u.second]
print(watertreated)

water = [2.64,0.052,0.165,0.056]
objects = ('Carbon', 'Charcoal', 'Charcoal w/ Salt', 'Sand')
y_pos = np.arange(len(watertreated))

plt.bar(y_pos, water, align='center', alpha=0.5)
plt.xticks(y_pos, objects)
plt.ylabel('Water Treated (L)')
plt.title('Water Treated by Method')

plt.show()
plt.savefig('C:/Users/dapmo/github/4530/data/Final/FINAL4')




```
