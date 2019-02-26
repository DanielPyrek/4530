```python

#DANEILEFA ANDS JESSICASPPWD


from aguaclara.core.units import unit_registry as u
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from scipy import stats

data_file_path = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranTime0_1"
data_file_path2 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranTime0_2"
data_file_path3 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranPlotF1"
from aguaclara.core.units import unit_registry as u
u.define('equivalent = mole = eq')
import aguaclara.research.environmental_processes_analysis as epa
from scipy import optimize

def ANC_zeroed(pHguess, ANC):
 return ((epa.ANC_open(pHguess) - ANC).to(u.mol/u.L)).magnitude


df = pd.read_csv(data_file_path,delimiter='\t')
df2 = pd.read_csv(data_file_path2,delimiter='\t')
df3 = pd.read_csv(data_file_path3,delimiter='\t')
print(df)
list(df)
columns = df.columns
print(columns)
x = df[list(df)[0]].values * u.ml
x
x = df.loc[:, list(df)[0]].values * u.ml
x
x = df.iloc[:,0].values * u.ml
x
y = df.iloc[:,1].values * u.pH


print(df2)
list(df2)
columns2 = df2.columns
print(columns2)
x2 = df2[list(df2)[0]].values * u.ml
x2
x2 = df2.loc[:, list(df2)[0]].values * u.ml
x2
x2= df2.iloc[:,0].values * u.ml
x2
y2 = df2.iloc[:,1].values * u.pH

fig, ax = plt.subplots()
 # plot the data as red circles
ax.plot(x2, y2, 'bo', )
ax.plot(x, y, 'ro', )




# Add axis labels using the column labels from the dataframe
ax.set(xlabel=list(df)[0])
ax.set(ylabel=list(df)[1])
ax.legend(['ANC = [HC03^-1] + 2[CO3^-2] + [OH-] - [H+] ', 'ANC = [HC03^-1] + [OH-] - [H+] '])
ax.grid(True)
# Here I save the file to my local harddrive. You will need to change this to work on your computer.
# We don't need the file type (png) here.

plt.savefig('C:/Users/dapmo/github/4530/Time0GranPlot')
plt.show()





# Question 2
print(df3)
list(df3)
columns3 = df3.columns
print(columns3)
x3 = df3[list(df2)[0]].values * u.mg/u.L
x3
x3 = df3.loc[:, list(df2)[0]].values * u.mg/u.L
x3
x3= df3.iloc[:,0].values * u.ml
x3
y3 = df3.iloc[:,1].values * u.ml

x4= df3.iloc[8:11,0].values * u.ml
x4
y4 = df3.iloc[8:11,1].values * u.dimensionless

slope, intercept, r_value, p_value, std_err = stats.linregress(x4,y4)

#We can add the units to intercept by giving it the same units as the y values.
intercept = intercept * y3.units
# Note that slope is dimensionless for this case, but not in general!
# For the general case we can attach the correct units to slope.
slope = slope * y3.units/x3.units
print(slope)
print(intercept)


fig, ax = plt.subplots()
 # plot the data as red circles
ax.plot(x3, y3, 'ro', )
ax.plot(x4, slope * x4 + intercept, 'k-', )

# Add axis labels using the column labels from the dataframe
ax.set(xlabel=list(df3)[0])
ax.set(ylabel=list(df3)[1])
ax.legend(['Titrant volume', 'Linear regression'])
ax.grid(True)
# Here I save the file to my local harddrive. You will need to change this to work on your computer.
# We don't need the file type (png) here.

plt.savefig('C:/Users/dapmo/github/4530/Time0GranPlotF1')
plt.show()

xintercept=(-intercept)/slope
xintercept


#Import lab ANC data
data_file_path5 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/ANCValues"
df5 = pd.read_csv(data_file_path5,delimiter='\t')
x5 = df5[list(df5)[0]].values * u.minutes
x5
x5 = df5.loc[:, list(df5)[0]].values * u.minutes
x5
x5 = df5.iloc[:,0].values * u.minute
x5 = x5.to(u.second)
x5
y5= df5.iloc[:,1].values * u.pH





#Recreate old graph ANC data
data_file_path4 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/Lab3.1"
from aguaclara.core.units import unit_registry as u
u.define('equivalent = mole = eq')
import aguaclara.research.environmental_processes_analysis as epa
from scipy import optimize

def ANC_zeroed(pHguess, ANC):
 return ((epa.ANC_open(pHguess) - ANC).to(u.mol/u.L)).magnitude

# Now we use root finding to find the pH that results in the known ANC.
# Our function will call the ANC_zeroed function. The pHguess is the first
# input of the ANC_zeroed function and the range on that is set by the next
# two inputs in the optimize.brentq function. The ANC is passed as an
# additional argument.
def pH_open(ANC):
 return optimize.brentq(ANC_zeroed, 0, 14,args=(ANC))

#Now we create a pandas dataframe with the data in the file
df = pd.read_csv(data_file_path4,delimiter='\t')
print(df)
list(df)
columns = df.columns
print(columns)
#Below are three equally fine methods of extracting a column of data from the pandas dataframe.

x = df[list(df)[0]].values * u.seconds
x
# 2) We can use the loc command to select all of the rows (: command) and the column with the label given by list(df)[0].
x = df.loc[:, list(df)[0]].values * u.seconds
x
# 3) We can use the iloc command and select all of the rows in column 0.
x = df.iloc[:,0].values * u.seconds
xtime = x
V = 4.17*u.L
Q = 0.005833*u.L/u.second
theta = V/Q
theta
x = x/theta*u.dimensionless
#The iloc method is simple and efficient, so I'll use that to get the y values.
y = df.iloc[:,1].values


#Question 2

Mass=623*u.mg
ANC0=Mass/V/(84*u.mg)/(1000)*u.equivalent
ANCIN = -0.000631*u.eq/u.L

y2 = y
y2 = ANCIN*(1-(2.71828**(-x).to(u.dimensionless).magnitude))+ANC0*2.71828**(-x).to(u.dimensionless).magnitude


# Add axis labels using the column labels from the dataframe
ax.set(xlabel="Residence Time (dimensionless)")
ax.set(ylabel="ANC (eq/L)")
ax.legend(['Conservative ANC'])
ax.grid(True)
# Here I save the file to my local harddrive. You will need to change this to work on your computer.
# We don't need the file type (png) here.

plt.savefig('C:/Users/dapmo/github/4530/Lab3Plot2')
plt.show()



Carb = .0017786
y3 = epa.ANC_closed(y,Carb*u.mol/u.L)
y4 = epa.ANC_open(y)

fig, ax = plt.subplots()
ax.plot(xtime, y3, 'blue' ,)
ax.plot(xtime, y4, 'green', )
ax.plot(xtime, y2, 'red', )
ax.plot(x5, y5, 'orange', )

# Add axis labels using the column labels from the dataframe
ax.set(xlabel="Residence Time (dimensionless)")
ax.set(ylabel="ANC (eq/L)")
ax.legend(['Closed ANC', 'Open ANC', 'Conservative ANC','Empirical ANC Data'])
ax.grid(True)
plt.savefig('C:/Users/dapmo/github/4530/Lab3Plot3')
plt.show()



```
