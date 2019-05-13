**Adsorption Lab**
**Group 8**
4/18/19
Daniel Pyrek - 5 hours
Jessie Powell - 5 hours

**1)** Here are the breakthrough curves for  the tests without any activated carbon. They seem quite consistent, each with fast breakthroughs. The  test at 2.6 microliters per second seemed to breakthrough faster than 2 out of 3 of the tests at 0.5 microliters per second. This could indicate that faster flow rates cause faster breakthroughs.
![plot](https://github.com/DanielPyrek/4530/blob/master//Sand_column.png?raw=true)
*Graph 1: Sand Breakthrough Curves*


Here is the breakthrough curve for the tests with activated carbon. The more carbon in the column, the longer it took for the test to breakthrough. The yellow line with 29.3 g of carbon took a very long time to breakthrough.
![plot](https://github.com/DanielPyrek/4530/blob/master//Adsorption.png?raw=true)
*Graph 2: Activated Carbon Breakthrough Curves*

**2)** Here is a plot showing the time when the effluent concentration 50% versus mass of activated carbon. It seems like the general trend is that the time to reach 50% increases with mass of activated carbon. This is especially apparent with the 29.3g of carbon test.
![plot](https://github.com/DanielPyrek/4530/blob/master//Adsorptiontimeto50.png?raw=true)
*Graph 3: Time till the effluent concentration was 50%*

**3)** The retardation factors for the 4 sand tests are: 1.60610114, 1.54779162, 1.2722501 , 1.23448781.These are all very low because sand did not do a good job at adsorbing the red dye.

The retardation factors for activated carbon are as follows: 1.29059221,   1.1186696 ,   3.57505897, 5.23205059, 0.66971197,   5.66348582,  23.58041714,   6.83584163, 171.07142729. These are increasing order of tests from least to most activated carbon. It is quite clear that increasing the mass of activated carbon increases the retardation factor. Adding less than a gram of carbon resembled pure sand whereas almost 30 grams of carbon increased the retardation factor to 171.

**4)** We calculated the value of qo for each of the columns based on equation (97). The mass of adsorbate per mass of adsorbent resembles graph 3. As the mass of activated increases, qo seemed to increase as well.

![plot](https://github.com/DanielPyrek/4530/blob/master//AdsorptionQ.png?raw=true)
*Graph 4: qo values versus Mass of Activated Carbon*


**Suggestions/Comments**
Overall, the lab was enjoyable and visually interesting. The initial set up was slightly confusing given the vast amount of tubing, valves, and other components necessary for a proper apparatus. However, with Jonathan’s own version of the set up next to us, we were able to finish building the experiment. Apart from that, our only issues were from the code during our post lab analysis. Some of the data varied in time collected and amount of carbon used, with made comparisons difficult to execute. Additionally, some of the code was complicated and required more python skill than we comfortably had. This included several if statements and nested for-loops for question #2. Otherwise, the adsorption lab was productive and aided us in our final experiment.

**Conclusion**
It was concluded that an increase in the amount of activated carbon (in mg/L) caused the adsorption curve to break through at a later point. Additionally, higher flow rates caused earlier breakthroughs. From the graphs, is seemed as though as activated carbon mass increased, two things happened: the time when the effluent concentration was 50% and q0 increased.  

**Appendix**


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
    C_data=[epa.column_of_data(i,epa.notes(i).last_valid_index() + 1,C_column,-1,'mg/L') for i in filepaths]
    time_data=[(epa.column_of_time(i,epa.notes(i).last_valid_index() + 1,-1)).to(u.s) for i in filepaths]

    adsorption_collection = collections.namedtuple('adsorption_results','metadata filenames C_data time_data')
    adsorption_results = adsorption_collection(metadata, filenames, C_data, time_data)
    return adsorption_results


C_column = 1
dirpath = "https://raw.githubusercontent.com/monroews/CEE4530/master/Examples/data/Adsorption"



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
        if C_data[i][k]/C_0 >= 0.5:
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
plt.savefig('C:/Users/dapmo/github/4530/Sand_column')
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
plt.savefig('C:/Users/dapmo/github/4530/Adsorption')

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
plt.savefig('C:/Users/dapmo/github/4530/AdsorptionQ')
plt.show()




plt.xlabel(r'$\frac{t}{\theta}$');
plt.xlim(right=100,left=0);
plt.ylabel(r'Red dye concentration $\left ( \frac{mg}{L} \right )$');
plt.legend(mylegend);
plt.savefig('C:/Users/dapmo/github/4530/Activated_carbon')
plt.show()
```
