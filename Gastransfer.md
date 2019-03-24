**Gas Transfer Post Lab**
**Group 8**
3/11/19
Daniel Pyrek - 9 hours
Jessie Powell - 8 hours

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
z = 5
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

C_star = (epa.O2_sat(P_air*z,temp))*(u.L/u.mg)
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
plt.xlabel(r'$time (s)$')
plt.ylabel(r'Oxygen concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Model','Recorded'])
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer3')
plt.show()

xx = (100,125,175,200,225,250,350,400,450,475,500,525,575,650,700,725,750,775,800,825,850,925,950)
plt.plot(xx,kvalues,'o')
plt.xlabel(r'$Flow Rate (muM/s)$')
plt.ylabel('k value')
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer4')
plt.show()


yy = []
for i in range(0,23):
  k = kvalues[i]
  Q = xx[i]
  V = 3
  R = 8.314
  T = 273+22
  MW = 32
  OTE = (k*6*V*R*T)/(.21*MW*P_air*Q)
  yy = np.append(yy,OTE)


plt.plot(xx,yy,'ro')
plt.xlabel('Flow Rate (muM/s)')
plt.ylabel('OTE')
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer5')
#delete data that is less than 2 or greater than 6 mg/L
plt.show()

```
**Data Analysis**

1) See appendix for code.
2) See figures 1 and 2 below:


![plot](https://github.com/DanielPyrek/4530/blob/master//GasTransfer.png?raw=true)
Figure 1. Dissolved Oxygen Concentration for Each Flow Rate


![plot](https://github.com/DanielPyrek/4530/blob/master//GasTransfer2.png?raw=true)
Figure 2. Dissolved Oxygen Concentration for 5 Flow Rates

At the beginning, most of the data sets look quite linear. From there they almost begin to plateau out like a log function. The slopes vary between the data sets.

3)
In order to solve for the C star, we used the O2 saturation function in epa.
$$Cstar = epa.O2sat(Pair,temp) = 8.412 mg/L$$

4)
Below are the k values for each flow rate:
Flow rate - K-values
100 - 0.00037139
125 - 0.00047827
175 - 0.00046432
200 - 0.00043635
225 - 0.00048833
250 - 0.00102538
350 - 0.00088487
400 - 0.00117507
450 - 0.00138456
475 - 0.00117248
500 - 0.00100520
525 - 0.00093568
575 - 0.00076105
650 - 0.00130161
700 - 0.00136895
725 - 0.00117918
750 - 0.00165133
775 - 0.00136205
800 - 0.00097218
825 - 0.00090033
850 - 0.00135607
925 - 0.00066758
950 - 0.00162662


5)
![plot](https://github.com/DanielPyrek/4530/blob/master//GasTransfer3.png?raw=true)
Figure 3. Dissolved Oxygen Concentration for Air Flow Rate of 100 micromole/s, Measured and Theoretical

The model fits the data for 100 muM/s very well. We used the following equation for the model:

$$ C = - (C^{*} - C_o)*e^{-kt} +  C^{*}  $$

6)
![plot](https://github.com/DanielPyrek/4530/blob/master//GasTransfer4.png?raw=true)
Figure 4. K-values of Flow Rates

K-values seem to increase with flowrate.

7)
![plot](https://github.com/DanielPyrek/4530/blob/master//GasTransfer5.png?raw=true)
Figure 5. Oxygen Transfer Efficiency for Air Flow Rates

Oxygen transfer efficiency seems to decrease with increased flow rate. This could be because the water is more saturated with oxygen so the transfer rate would decrease. It could also be because the bubbles are larger or the flow is too fast for the oxygen to be efficient.

8. There is a downward trend in amount of oxygen transfer efficiency as the air flow rate increases. It appears to be linearly related.


9. There are several ways to increase the efficiency of the experimental apparatus. Assuming another container is available, increasing the size of the lake is one way to help increase efficiency. Additionally, one could increase the temperature or decrease flow rate.

**Conclusions**
Through the Gas Transfer Lab/Experiment, it was seen that dissolved oxygen (DO) concentration increased quicker at higher flow rates. Additionally, by use of a pressure sensor for the accumulator and measuring the approximate volume, it was found that the oxygen transfer efficiency (OTE) decreases with an increase in air flow rate.

**Suggestions/Comments**
The gas transfer improved when doing it second time. The instructions for calibrating the DO probe and air flow controller were much clearer and included more details and steps which were confusing or missed on the first attempt. One suggestion involves the needle valve located closest to the lake. It was unclear approximately how much air should be flowing out of the aerator. Although told to turn the needle valve about forty degrees open, it was difficult to get an accurate flow. Perhaps a more labeled knob on the valve would help get a more precise flow. Additionally, this particular lab required a significant amount of coding skills with python, which may leave some individuals at a disadvantage; more premade functions, examples, or additional time to complete would be helpful.





**Appendix:**


from aguaclara.core.units import unit_registry as u
import aguaclara.research.environmental_processes_analysis as epa
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats
import collections
import os
from pathlib import Path

This code is included because there is a bug in the version of this code that is in epa.

def aeration_data(DO_column, dirpath):

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



 The column of data containing the dissolved oxygen concentrations
DO_column = 2
acc_column = 1
dirpath = "data/Aeration/"
filepaths, airflows, DO_data, time_data = aeration_data(DO_column,dirpath)
Accumulator = []
z = 5
 Plot the raw data
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

C_star = (epa.O2_sat(P_air*z,temp))*(u.L/u.mg)
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
C=-k.to(u.dimensionless).magnitude*t.to(u.dimensionless).magnitude+DOdata[7]


plt.plot(t,C,'g')
plt.plot(timedata,DOdata,'ro')
plt.xlabel(r'$time (s)$')
plt.ylabel(r'Oxygen concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Model','Recorded'])
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer3')
plt.show()

xx = (100,125,175,200,225,250,350,400,450,475,500,525,575,650,700,725,750,775,800,825,850,925,950)
plt.plot(xx,kvalues,'o')
plt.xlabel(r'$Flow Rate (muM/s)$')
plt.ylabel('k value')
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer4')
plt.show()


yy = []
for i in range(0,23):
  k = kvalues[i]
  Q = xx[i]
  V = 3
  R = 8.314
  T = 273+22
  MW = 32
  OTE = (k*6*V*R*T)/(.21*MW*P_air*Q)
  yy = np.append(yy,OTE)


plt.plot(xx,yy,'ro')
plt.xlabel('Flow Rate (muM/s)')
plt.ylabel('OTE')
plt.savefig('C:/Users/dapmo/github/4530/GasTransfer5')
delete data that is less than 2 or greater than 6 mg/L
plt.show()
