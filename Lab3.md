```python
  from aguaclara.core.units import unit_registry as u
  import numpy as np
  import matplotlib.pyplot as plt
  import pandas as pd
  from scipy import stats
  #The data file path is the raw data url on github. Happily python can read directly from a web page.
  data_file_path = "https://raw.githubusercontent.com/DanielPyrek/4530/master/Lab3_1"
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
  df = pd.read_csv(data_file_path,delimiter='\t')
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
  x
  V = 4.17*u.L
  Q = 0.005833*u.L/u.second
  theta = V/Q
  x = x/theta*u.dimensionless
  #The iloc method is simple and efficient, so I'll use that to get the y values.
  y = df.iloc[:,1].values
  # We will use the stats package to do the linear regression.
  # It is important to note that the units are stripped from the x and y arrays when processed by the stats package.

  # Now create a figure and plot the data and the line from the linear regression.
  fig, ax = plt.subplots()
  # plot the data as red circles
  ax.plot(x, y, 'ro', )


  # Add axis labels using the column labels from the dataframe
  ax.set(xlabel="Residence Time (dimensionless)")
  ax.set(ylabel=list(df)[1])
  ax.legend(['Measured', 'Linear regression'])
  ax.grid(True)
  # Here I save the file to my local harddrive. You will need to change this to work on your computer.
  # We don't need the file type (png) here.

  plt.savefig('C:/Users/dapmo/github/4530/Lab3Plot1')
  plt.show()




#Question 2

Mass=623*u.mg
ANC0=Mass/V/(84*u.mg)/(1000)*u.equivalent
ANCIN = 0*u.eq/u.L

y2 = y
y2 = ANC0*2.71828**(-x).to(u.dimensionless).magnitude

fig, ax = plt.subplots()
# plot the data as red circles
ax.plot(x, y2, 'ro', )


# Add axis labels using the column labels from the dataframe
ax.set(xlabel="Residence Time (dimensionless)")
ax.set(ylabel="ANC (eq/L)")
ax.legend(['Conservative ANC'])
ax.grid(True)
# Here I save the file to my local harddrive. You will need to change this to work on your computer.
# We don't need the file type (png) here.

plt.savefig('C:/Users/dapmo/github/4530/Lab3Plot2')
plt.show()




#Questions 3 and 4
Carb = .0017786
y3 = epa.ANC_closed(y,Carb*u.mol/u.L)
y4 = epa.ANC_open(y)

fig, ax = plt.subplots()
ax.plot(x, y3, 'blue' ,)
ax.plot(x, y4, 'green', )

# Add axis labels using the column labels from the dataframe
ax.set(xlabel="Residence Time (dimensionless)")
ax.set(ylabel="ANC (eq/L)")
ax.legend(['Closed ANC', 'Open ANC'])
ax.grid(True)
plt.savefig('C:/Users/dapmo/github/4530/Lab3Plot3')
plt.show()



data_file_path2 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/Lab3_2"
#Now we create a pandas dataframe with the data in the file
df = pd.read_csv(data_file_path2,delimiter='\t')
print(df)
list(df)
columns = df.columns
print(columns)
#Below are three equally fine methods of extracting a column of data from the pandas dataframe.

xc = df[list(df)[0]].values * u.seconds
xc
# 2) We can use the loc command to select all of the rows (: command) and the column with the label given by list(df)[0].
xc = df.loc[:, list(df)[0]].values * u.seconds
xc
# 3) We can use the iloc command and select all of the rows in column 0.
xc = df.iloc[:,0].values * u.seconds
xc
V = 4.17*u.L
Q = 0.005833*u.L/u.second
theta = V/Q
xc = xc/theta*u.dimensionless
#The iloc method is simple and efficient, so I'll use that to get the y values.
yc = df.iloc[:,1].values

fig, ax = plt.subplots()
# plot the data as red circles
ax.plot(xc, yc, 'ro', )


# Add axis labels using the column labels from the dataframe
ax.set(xlabel="Residence Time (dimensionless)")
ax.set(ylabel=list(df)[1])
ax.legend(['Measured', 'Linear regression'])
ax.grid(True)
# Here I save the file to my local harddrive. You will need to change this to work on your computer.
# We don't need the file type (png) here.

plt.savefig('C:/Users/dapmo/github/4530/Lab3Plot4')
plt.show()

  ```
Lab 3 Part 1
Daniel Pyrek
Jessie Powell

1.
  ![plot](https://github.com/DanielPyrek/4530/blob/master/Lab3Plot1.png?raw=true)
      Figure 1: Lake pH vs Hydraulic Residence Time

2.
  ![plot](https://github.com/DanielPyrek/4530/blob/master/Lab3Plot2.png?raw=true)
          Figure 2: Expected ANC vs Hydraulic Residence Time

$$ANC_{out} \; =\; ANC_{in} \; \cdot \; \left(1\; -\; {\mathop{e}\nolimits^{-t/\theta \; \; }} \right)+\; ANC_{0} \; \cdot \; {\mathop{e}\nolimits^{-t/\theta \; }}$$

3&4.
  ![plot](https://github.com/DanielPyrek/4530/blob/master/Lab3Plot3.png?raw=true)
              Figure 3: Closed and Open ANC vs Hydraulic Residence Time

  We used the environmental_processes_analysis functions to solve for #3 and #4. Specifically the epa.ANC_closed and epa.ANC_open


5.
  ![plot](https://github.com/DanielPyrek/4530/blob/master/Lab3Plot4.png?raw=true)
                  Figure 4: Lake pH vs Hydraulic Residence Time for Calcium Carbonate


The pH dropped a lot faster for the calcium carbonate versus when we used sodium carbonate. This indicates that the calcium carbonate has a lower ANC than the sodium carbonate. Therefore the acid rain was able to neutralize it quicker and drop the pH faster.
