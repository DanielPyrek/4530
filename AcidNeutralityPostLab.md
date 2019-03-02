```python

#DanielPyrek and JessiePowell


from aguaclara.core.units import unit_registry as u
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from scipy import stats
import numpy

data_file_path = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranTime0_1"
data_file_path2 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranTime0_2"
data_file_path3 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranPlotF1"
from aguaclara.core.units import unit_registry as u
u.define('equivalent = mole = eq')
import aguaclara.research.environmental_processes_analysis as epa
from scipy import optimize

def ANC_zeroed(pHguess, ANC):
 return ((epa.ANC_open(pHguess) - ANC).to(u.mol/u.L)).magnitude

#Question1

#Import data for titration curve
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
y

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
y2
df = pd.read_csv(data_file_path2,delimiter='\t')
x8 = df[list(df)[0]].values * u.ml
x8
x8 = df.loc[:, list(df)[0]].values * u.ml

x10=[1.75,2]*u.ml
y10=[5.17327,3.98137]*u.pH

x10
y10
  # Plot
fig, ax = plt.subplots()
ax.plot(x2, y2, 'blue', )
ax.plot(x, y, 'red', )
ax.plot(x10, y10, 'purple', )
ax.set(xlabel=list(df)[0])
ax.set(ylabel=list(df)[1])
ax.legend(['ANC = [HC03^-1] + [OH-] - [H+] ','ANC = [HC03^-1] + 2[CO3^-2] + [OH-] - [H+] ','Steep Slope'])
ax.grid(True)
plt.savefig('C:/Users/dapmo/github/4530/Final')
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


#Linear regression
slope, intercept, r_value, p_value, std_err = stats.linregress(x4,y4)
intercept = intercept * y3.units
slope = slope * y3.units/x3.units
print(slope)
print(intercept)

#Plot
fig, ax = plt.subplots()
ax.plot(x3, y3, 'ro', )
ax.plot(x4, slope * x4 + intercept, 'k-', )
ax.set(xlabel=list(df3)[0])
ax.set(ylabel=list(df3)[1])
ax.legend(['Titrant volume', 'Linear regression'])
ax.grid(True)
plt.savefig('C:/Users/dapmo/github/4530/Time0GranPlotF1')
plt.show()

#Solve for Ve
xintercept=(-intercept)/slope
xintercept



#Question3

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




Carb = .0017786
y3 = epa.ANC_closed(y,Carb*u.mol/u.L)
y4 = epa.ANC_open(y)


#Plot
fig, ax = plt.subplots()
ax.plot(xtime, y3, 'blue' ,)
ax.plot(xtime, y4, 'green', )
ax.plot(xtime, y2, 'red', )
ax.plot(x5, y5, 'orange', )

ax.set(xlabel="Residence Time (dimensionless)")
ax.set(ylabel="ANC (eq/L)")
ax.legend(['Closed ANC', 'Open ANC', 'Conservative ANC','Empirical ANC Data'])
ax.grid(True)
plt.savefig('C:/Users/dapmo/github/4530/Lab4ANCPlot')
plt.show()




```
<b>Acid Neutrality Post Lab3
Daniel Pyrek and Jessie Powell
3/2/19</b>
<br>

<b>Introduction and Objectives</b>
	The goal of this lab is to determine ANC of all the samples recovered from the previous lab, Acid Lake Remediation Lab. From that, five 50mL samples from the “lake” were recovered, each taken at five minute time intervals with increasing amounts of the acid NaOH, which has a pH of 3.2. To find the ANC, hydrochloric acid was added incrementally and recording data on a Gran plot. From the plots, it is possible to determine the exact volume of titrant needed and from there, the ANC, which is a function of said volume:
<br>
$$ANC=\frac{V_e N_t }{V_s }$$

<br>

<b>Procedures</b>
	To begin, the pH probe was calibrated using pH 4,7 and 10 buffers. Once calibrated, the ANC of 50 mL of reverse osmosis water was measured to verify that the Gran technique works accurately. To test this, the beaker was placed on the stirrer with stir bar. Then the initial pH was measured, followed by the first 0.25 mL addition of hydrochloric acid. The pH was recorded after each titrant addition. This procedure was repeated with all five samples.
<br>
<b>Results</b>

<u>Task 1</u>
<br>
Our first task was to plot a titration curve from the data we collected. We plotted pH as a function of titrant volume on Plot 1 below. This is important because we can monitor what reactions are occurring in our solution. We noticed that at higher pH values, all concentrations were accounted for in the ANC equation (the red line). However, after a steep drop off (the purple line), carbonate no longer was accounted for (the blue line). If our graph went to even lower pH values, only hydrogen ions would effect the ANC.
<br>
  ![plot](https://github.com/DanielPyrek/4530/blob/master//Final.png?raw=true)

  <i> Plot 1: pH vs Titrant Volume</i>


<u>Task 2</u>

Our next step was to create a Gran plot with data we collected from the titration curve at time = 0 in Plot 2 below. We took data in lab until we had three linear lines. The reason for the flat line at the beginning was that ANC was keeping the pH stable. The linear regression formed had a slope of 0.001232 and a y-intercept of -0.002351 mL. The Ve measured was 1.9083 mL. This is incredibly similar to ProCoda’s calculated Ve, which was 1.908638 mL.

Linear regression line: f(x)=0.001232x-0.002351
<br>

  ![plot](https://github.com/DanielPyrek/4530/blob/master//Time0GranPlotF1.png?raw=true)
<i> Plot 2: r1 vs Titrant Volume</i>

<br>
Below in Table 1 are the calculated values ProCoda gave us. This includes an ANC of 0.001909 (eq/L). The correlation coefficient was .99974 which means that the line was almost perfectly linear.

<br>

<table style="width:100%">
  <tr>
    <th>PROCODA VALUES</th>
  </tr>
  <tr>
    <td>Sample Volume (ml)</td>
    <td>50</td>

  </tr>
  <tr>
    <td>Titrant normality</td>
    <td>0.05</td>

  </tr>
  <tr>
    <td>Equivalent Volume (ml)</td>
    <td>1.90863</td>

  </tr>
  <tr>
    <td>ANC (eq/L)</td>
    <td>0.001909</td>

  </tr>
  <tr>
    <td>correlation coefficient</td>
    <td>0.99974</td>

  </tr>
</table>
<i>Table 1: ProCoda Values</i>
<br>
<br>
<br>


<u>Task 3</u>

 The final task we wanted to undertake was compare our experimental data with the models we made in the prelab. We plotted these lines on plot 3 below. We compared the yellow empirical ANC data line with the red conservative ANC model line. The measured ANC followed a similar trend to the conservative ANC model. The initial ANC for the measured data was slightly higher, but at time increases it becomes lower than the conservative data. Nonetheless, the curves are a close match in terms of shape and descent.
![plot](https://github.com/DanielPyrek/4530/blob/master/Lab4ANCPlot.png?raw=true)
<i> Plot 3: Comparing Empirical ANC and Conservative ANC Model </i>
<br>




<b>Conclusions</b>

  The aim of this lab experiment was to determine the acid neutralizing capacity of the lake samples from the previous lab experiment. Through incremental titrant addition of hydrochloric acid, and the use of the Gran plot in ProCoda, the specific volume of titrant necessary was found to find the ANC.

  <b>Suggestions/Comments</b>
  While setting up the lab within ProCoda, it was unclear what volume of titrant should be added incrementally. While it was eventually determined that .25 mL should be used per titration, perhaps it would be easier to state that within the lab procedures so it is clearer.

  ProCoda crashed on us several times. However, since this lab, bug fixes seem to have remedied this problem.

  <br>
  <b>Appendix</b>

  #DanielPyrek and JessiePowell


  from aguaclara.core.units import unit_registry as u
  import numpy as np
  import matplotlib.pyplot as plt
  import pandas as pd
  from scipy import stats
  import numpy

  data_file_path = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranTime0_1"
  data_file_path2 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranTime0_2"
  data_file_path3 = "https://raw.githubusercontent.com/DanielPyrek/4530/master/GranPlotF1"
  from aguaclara.core.units import unit_registry as u
  u.define('equivalent = mole = eq')
  import aguaclara.research.environmental_processes_analysis as epa
  from scipy import optimize

  def ANC_zeroed(pHguess, ANC):
   return ((epa.ANC_open(pHguess) - ANC).to(u.mol/u.L)).magnitude

  # Question 1

  #Import data for titration curve
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
  y

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
  y2
  df = pd.read_csv(data_file_path2,delimiter='\t')
  x8 = df[list(df)[0]].values * u.ml
  x8
  x8 = df.loc[:, list(df)[0]].values * u.ml

  x10=[1.75,2]*u.ml
  y10=[5.17327,3.98137]*u.pH

  x10
  y10
    # Plot
  fig, ax = plt.subplots()
  ax.plot(x2, y2, 'blue', )
  ax.plot(x, y, 'red', )
  ax.plot(x10, y10, 'purple', )
  ax.set(xlabel=list(df)[0])
  ax.set(ylabel=list(df)[1])
  ax.legend(['ANC = [HC03^-1] + [OH-] - [H+] ','ANC = [HC03^-1] + 2[CO3^-2] + [OH-] - [H+] ','Steep Slope'])
  ax.grid(True)
  plt.savefig('C:/Users/dapmo/github/4530/Final')
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


  #Linear regression
  slope, intercept, r_value, p_value, std_err = stats.linregress(x4,y4)
  intercept = intercept * y3.units
  slope = slope * y3.units/x3.units
  print(slope)
  print(intercept)

  #Plot
  fig, ax = plt.subplots()
  ax.plot(x3, y3, 'ro', )
  ax.plot(x4, slope * x4 + intercept, 'k-', )
  ax.set(xlabel=list(df3)[0])
  ax.set(ylabel=list(df3)[1])
  ax.legend(['Titrant volume', 'Linear regression'])
  ax.grid(True)
  plt.savefig('C:/Users/dapmo/github/4530/Time0GranPlotF1')
  plt.show()

  #Solve for Ve
  xintercept=(-intercept)/slope
  xintercept



  # Question 3

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

  #Now we use root finding to find the pH that results in the known ANC.
  #Our function will call the ANC_zeroed function. The pHguess is the first
  #input of the ANC_zeroed function and the range on that is set by the next
  #two inputs in the optimize.brentq function. The ANC is passed as an
  #additional argument.
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
  #2) We can use the loc command to select all of the rows (: command) and the column with the label given by list(df)[0].
  x = df.loc[:, list(df)[0]].values * u.seconds
  x
  #3) We can use the iloc command and select all of the rows in column 0.
  x = df.iloc[:,0].values * u.seconds
  xtime = x
  V = 4.17*u.L
  Q = 0.005833*u.L/u.second
  theta = V/Q
  theta
  x = x/theta*u.dimensionless
  #The iloc method is simple and efficient, so I'll use that to get the y values.
  y = df.iloc[:,1].values



  Mass=623*u.mg
  ANC0=Mass/V/(84*u.mg)/(1000)*u.equivalent
  ANCIN = -0.000631*u.eq/u.L

  y2 = y
  y2 = ANCIN*(1-(2.71828**(-x).to(u.dimensionless).magnitude))+ANC0*2.71828**(-x).to(u.dimensionless).magnitude


  #Add axis labels using the column labels from the dataframe
  ax.set(xlabel="Residence Time (dimensionless)")
  ax.set(ylabel="ANC (eq/L)")
  ax.legend(['Conservative ANC'])
  ax.grid(True)




  Carb = .0017786
  y3 = epa.ANC_closed(y,Carb*u.mol/u.L)
  y4 = epa.ANC_open(y)


  #Plot
  fig, ax = plt.subplots()
  ax.plot(xtime, y3, 'blue' ,)
  ax.plot(xtime, y4, 'green', )
  ax.plot(xtime, y2, 'red', )
  ax.plot(x5, y5, 'orange', )

  ax.set(xlabel="Residence Time (dimensionless)")
  ax.set(ylabel="ANC (eq/L)")
  ax.legend(['Closed ANC', 'Open ANC', 'Conservative ANC','Empirical ANC Data'])
  ax.grid(True)
  plt.savefig('C:/Users/dapmo/github/4530/Lab4ANCPlot')
  plt.show()
