
**Reactor Lab**
**Group 8**
3/25/19
Daniel Pyrek - 7 hours
Jessie Powell - 5 hours


**Introduction and Objectives:**
The goal of the reactor laboratory experiment was to play with different variables within a reactor, such as the number of baffles, number of holes within each baffle, hole size, and hole location through baffles. Through different variations, it was possible to see what components contributed to mixing capabilities. This was measured using a photometer near the outlet that would record the concentration of red dye, released via a pulse at the water inlet, as it passed through. The reactors tested included: a simple non-baffled CMFR, two baffles with four holes each along the same side, one baffle with four holes, and one baffle with 24 holes. These were chosen randomly, and because taping each additional baffle into the reactor took time and precision. Ultimately, the results of this lab illuminated ways to create more efficiently mixed reactors for life application.

**Procedures:**
An in depth description of the lab steps were outlined here: https://github.com/monroews/CEE4530/wiki/Lab-Reports. A photometer was added near the outlet of the reactor. A peristaltic pump was set at a flowrate of 380 mL/min, and filled the container that would serve as our reactor to approximately 2.25 liters. For the initial CMFR run, 6.75 milliliters of red dye #40, which is diluted to 10 grams/liter. This was added via a pulse near the water inlet. The concentration was recorded from the photometer over time. This was repeated with the additional reactor designs, except that the amount of the pulse was reduced to 1 milliliter. The three experiments with baffles were as follows (described briefly in the introduction): two baffles with four 1 centimeter vertically stacked holes each along the same side, one baffle with four 1 centimeter holes, and one baffle with 24 0.5 centimeter holes. For the experiment with two baffles, they were equally separated.


**Results and Discussion:**

**Data Analysis:**
1.

See appendix code.

2.

Here are the plots we generated showing experimental data as points and the model results as lines:

 ![plot](https://github.com/DanielPyrek/4530/blob/master//CMFR.png?raw=true)
 Plot 1: CMFR

 The best fit is the CMFR model which makes sense because this was a CMFR test.


 ![plot](https://github.com/DanielPyrek/4530/blob/master//Reactor_4x1cmholes_sealed_1mldye_1baffle.png?raw=true)
 Plot 2: 1 baffle with 4 1cm holes

The best fit for this test was the advection dispersion model. However, this is a close call. This makes sense because even though the Tstar value was small, it was still sufficient enough to make advection and dispersion matter.

 ![plot](https://github.com/DanielPyrek/4530/blob/master//Reactor_24x_5cmholes_sealed_1mldye_1baffle.png?raw=true)
Plot 3: 1 baffle with 24 .5cm holes

 The best fit for this test was the advection dispersion model. This makes sense because the Tstar is really large.


 ![plot](https://github.com/DanielPyrek/4530/blob/master//Reactor2BaffleTest_4x0_5cm.png?raw=true)
 Plot 4: 2 baffles with 4 1cm holes

 The best fit for this test was the CMFR model. This does not male much sense. However it does once we figured out that we messed up this experiment. We put both baffles with the holes on the same side. Therefore the value for Tstar was really low. So therefore advection and dispersion did not play a large role in this test.

3.

The estimated value of N for our CMFR is 1.19.
The estimated value of Pe for 1 baffle with 4 holes is 0.57.
The estimated value of Pe for 1 baffle with 24 holes is 5.27.
The estimated value of Pe for two baffles with 4 holes on one side is 3.03.

$$Pe=2N$$

In order to make the values make sense, we rounded the value of N for the CMFR and ceiling each other value of N:

The estimated value of N for our CMFR is 1.
The estimated value of N for 1 baffle with 4 holes is 1.
The estimated value of N for 1 baffle with 24 holes is 3.
The estimated value of N for two baffles with 4 holes on one side is 2.

The predicted values of N actually the number of reactors in series we had for each test once we rounded. Larger values of N increased dispersion amongst our tests.



4.


We can use this equation to get E(t) from C(t):
$$E_{\left(t^{\star} \right)} =\frac{{\rm C(x,t)}\rlap{-} V }{{\rm M}}$$


From there we can integrate to find
$$F_{\left(t^{\star} \right)} =\int _{0}^{t^{\star} }E_{\left(t^{\star} \right)} dt^{\star}$$

V = Volume of reactor
M = mass of pulse

We used a max function in Python to find C(Tin) and calculated C(Tstar). From there we used a for loop to find the time associated with it. We then divided by residence time to get Tstar. Here are the values for our tests:

The value of Tstar for our CMFR is 0.1425.
The value of Tstar for 1 baffle with 4 holes is 0.2348.
The value of Tstar for 1 baffle with 24 holes is 0.8773.
The value of Tstar for two baffles with 4 holes on one side is 0.1035.

When looking at table 1 below, we can compare the Tstar values we got in lab with what we should expect. Our CMFR got a Tstar of .1425 which is very close the expected value of 0.1. Our single baffle with 4 holes got a 0.235. This makes sense because one baffle with only a couple holes would be around the 0.1 - 0.3 range being 'poorly baffled'. Tbe 1 baffle with 24 small holes got a Tstar value of 0.88. This value huge. This means that one baffle with many small holes is already between 'superior' and 'perfect' baffling. The last test with two baffles with four holes got a value of 0.1035. This does not make sense because it is very small. However, we messed up this test run. We put the holes of the baffles on the same side of the reactor. Therefore the baffling was very ineffective.




   ![plot](https://github.com/DanielPyrek/4530/blob/master//Tstar.PNG?raw=true)
   Table 1: Tstar Values

 5. There were likely "dead volumes" or "short circuiting" in the first reactor test. In this test, two baffles were used, both with four holes stacked to one side. The "dead volume" occurred because the baffles were placed with the holes on the same side. Because of this, there was a lack of mixing between the baffles. This is where the dead volume took place.


6. Our results showed that an increase in baffles and holes, as well as a decrease in the diameter of said holes, seemed to increase the mixing potential in a reactor. We would recommend a full scale chlorine contact tank with many baffles and lots of small holes. Our highest Tstar occurred with a baffled reactor with 24 holes at 0.5 cm in diameter,  further suggesting this recommendation.

**Conclusions:**
Through the Reactor Lab/Experiment, it was seen that the addition of baffles and holes resulted in more mixing of red dye within in the reactor. Additionally it was noted that reactors with lower Tstar values were poorly mixed, or had "dead volumes".

**Suggestions/Comments:**
The lab manual for this experiment was fairly easy to follow. One problem that occurred involved the amount of dye that should be pulsed into the reactor. Perhaps it was simply misread, but initially it was decided that the amount and concentration of dye would need to be calculated based on the amount of water in the reactor. However, after doing this once, it was made known that only 1 mL needed to be added per pulse. Therefore, some additional clarity would be helpful for future labs. For the data analysis, it was helpful to have the reactor example that was uploaded. One last suggestion involved the topic of “dead volumes” and “short circuits”. While the concept was mentioned in the prior class period, it was not explicit what dead volumes were or reactor characteristics that should be avoided to prevent them.


**Appendix:**
```python

from aguaclara.core.units import unit_registry as u
import aguaclara.research.environmental_processes_analysis as epa
import aguaclara.core.utility as ut
import numpy as np
import matplotlib.pyplot as plt
from scipy import integrate

#The following file is from a CMFR
CMFR_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor30Test.xls'

# find the row after the last note in the file. This assumes that the last note marks the beginning of the test.
epa.notes(CMFR_path)
CMFR_firstrow = epa.notes(CMFR_path).last_valid_index() + 1
CMFR_firstrow

#I eliminate the beginning of the data file because this is a CMFR and the
#first data was taken before the dye reached the sensor. Note that eliminating
#some data from the beginning of the data file will not change the analysis
#except in the estimate of the initial tracer mass.#
CMFR_firstrow = CMFR_firstrow + 10


CMFR_time_data = (epa.column_of_time(CMFR_path,CMFR_firstrow,-1)).to(u.s)

CMFR_concentration_data = epa.column_of_data(CMFR_path,CMFR_firstrow,1,-1,'mg/L')



#I don't actually know the values that follow. I'm guessing.
#You should use real measured values!#
CMFR_V = 2.25*u.L
CMFR_Q = 380 * u.mL/u.min

#here we set estimates that we will use as starting values for the curve fitting
CMFR_theta_hydraulic = (CMFR_V/CMFR_Q).to(u.s)
CMFR_C_bar_guess = np.max(CMFR_concentration_data)

#The Solver_CMFR_N will return the initial tracer concentration,
#residence time, and number of reactors in series.
#This experiment was for a single reactor and so we expect N to be 1!
CMFR_CMFR = epa.Solver_CMFR_N(CMFR_time_data, CMFR_concentration_data, CMFR_theta_hydraulic, CMFR_C_bar_guess)
#use dot notation to get the 3 elements of the tuple that are in CMFR.

print('The model estimated mass of tracer injected was',ut.round_sf(CMFR_CMFR.C_bar*CMFR_V ,2) )
print('The model estimate of the number of reactors in series was', CMFR_CMFR.N)
print('The tracer residence time was',ut.round_sf(CMFR_CMFR.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(CMFR_CMFR.theta/CMFR_theta_hydraulic).magnitude)

M = (10*u.g/u.L).to(u.mg/u.ml)*6.75*u.ml
#Save CT(in)
E1 = CMFR_concentration_data*CMFR_V/(M)


tstarvalues=CMFR_time_data/(ut.round_sf(CMFR_CMFR.theta ,2))

F1 = integrate.cumtrapz(E1,tstarvalues)

value = min(F1, key=lambda x:abs(x-.1))

#Calculate Tstar
place = 0
for i in [i for i,x in enumerate(F1) if x == value]:
  place = i
  if place != 0:
   break
tstarcmfr=tstarvalues[place]
print('The value for Tstar is',(tstarcmfr))


#create a model curve given the curve fit parameters.

CMFR_CMFR_model = CMFR_CMFR.C_bar * epa.E_CMFR_N(CMFR_time_data/CMFR_CMFR.theta,CMFR_CMFR.N)
plt.plot(CMFR_time_data.to(u.min), CMFR_concentration_data.to(u.mg/u.L),'ro')
plt.plot(CMFR_time_data.to(u.min), CMFR_CMFR_model,'b')

plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model'])
plt.savefig('C:/Users/dapmo/github/4530/CMFR', bbox_inches = 'tight')
plt.show()

#Load a data file for a reactor with baffles.

one_baffle_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor_4x1cmholes_sealed_1mldye_1baffle.xls'
one_baffle_firstrow = epa.notes(one_baffle_path).last_valid_index() + 1
one_baffle_time_data = (epa.column_of_time(one_baffle_path,one_baffle_firstrow,-1)).to(u.s)
one_baffle_concentration_data = epa.column_of_data(one_baffle_path,one_baffle_firstrow,1,-1,'mg/L')

#I noticed that the initial concentration measured by the photometer wasn't
#zero. This suggests that there may have been a small air bubble in the
#photometer or perhaps there was some other anomoly that was causing the
#photometer to read a concentration that was higher than was actually present in
#the reactor. To correct for this I subtracted the initial concentration reading
#from all of the data. This was based on the assumption that the concentration
#measurement error persisted for the entire experiment.#

one_baffle_concentration_data = one_baffle_concentration_data - one_baffle_concentration_data[0]
one_baffle_V = 2.25*u.L
one_baffle_Q = 380 * u.mL/u.min
one_baffle_theta_hydraulic = (one_baffle_V/one_baffle_Q).to(u.s)
one_baffle_C_bar_guess = np.max(one_baffle_concentration_data)/2
#use solver to get the CMFR parameters
one_baffle_CMFR = epa.Solver_CMFR_N(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_CMFR.C_bar
one_baffle_CMFR.N
one_baffle_CMFR.theta.to(u.s)

#Create the CMFR model curve based on the scipy.optimize curve_fit
#parameters. We do this with dimensions so that we can plot both models and
#the data on the same graph. If we did this in dimensionless space it wouldn't
#be possible to plot everything on the same plot because the values used to
#create dimensionless time and dimensionless concentration are different for
#the two models.

one_baffle_CMFR_model = (one_baffle_CMFR.C_bar*epa.E_CMFR_N(one_baffle_time_data/one_baffle_CMFR.theta, one_baffle_CMFR.N)).to(u.mg/u.L)

#use solver to get the advection dispersion parameters
one_baffle_AD = epa.Solver_AD_Pe(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_AD.C_bar
one_baffle_AD.Pe
one_baffle_AD.theta

print('The model estimated mass of tracer injected was',ut.round_sf(one_baffle_AD.C_bar*one_baffle_V ,2) )
print('The model estimate of the Peclet number was', one_baffle_AD.Pe)
print('The tracer residence time was',ut.round_sf(one_baffle_AD.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(one_baffle_AD.theta/one_baffle_theta_hydraulic).magnitude)

#Create the advection dispersion model curve based on the solver parameters
one_baffle_AD_model = (one_baffle_AD.C_bar*epa.E_Advective_Dispersion((one_baffle_time_data/one_baffle_AD.theta).to_base_units(), one_baffle_AD.Pe)).to(u.mg/u.L)

#Plot the data and the two model curves.
plt.plot(one_baffle_time_data.to(u.s), one_baffle_concentration_data.to(u.mg/u.L),'ro')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_CMFR_model,'b')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
plt.savefig('C:/Users/dapmo/github/4530/Reactor_4x1cmholes_sealed_1mldye_1baffle', bbox_inches = 'tight')
plt.show()


M = (10*u.g/u.L).to(u.mg/u.ml)*1*u.ml
#Save CT(in)
E2 = one_baffle_concentration_data*CMFR_V/(M)


tstarvalues=one_baffle_time_data/(ut.round_sf(one_baffle_AD.theta ,2))

F2 = integrate.cumtrapz(E2,tstarvalues)

value = min(F2, key=lambda x:abs(x-.1))

#Calculate Tstar
place = 0
for i in [i for i,x in enumerate(F2) if x == value]:
  place = i
  if place != 0:
   break
tstar=tstarvalues[place]
print('The value for Tstar is',(tstar))



#Load 2nd file

one_baffle_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor_24x_5cmholes_sealed_1mldye_1baffle.xls'
one_baffle_firstrow = epa.notes(one_baffle_path).last_valid_index() + 1
one_baffle_time_data = (epa.column_of_time(one_baffle_path,one_baffle_firstrow,-1)).to(u.s)
one_baffle_concentration_data = epa.column_of_data(one_baffle_path,one_baffle_firstrow,1,-1,'mg/L')

#I noticed that the initial concentration measured by the photometer wasn't
#zero. This suggests that there may have been a small air bubble in the
#photometer or perhaps there was some other anomoly that was causing the
#photometer to read a concentration that was higher than was actually present in
#the reactor. To correct for this I subtracted the initial concentration reading
#from all of the data. This was based on the assumption that the concentration
#measurement error persisted for the entire experiment.#

one_baffle_concentration_data = one_baffle_concentration_data - one_baffle_concentration_data[0]
one_baffle_V = 2.25*u.L
one_baffle_Q = 380 * u.mL/u.min
one_baffle_theta_hydraulic = (one_baffle_V/one_baffle_Q).to(u.s)
one_baffle_C_bar_guess = np.max(one_baffle_concentration_data)/2
#use solver to get the CMFR parameters
one_baffle_CMFR = epa.Solver_CMFR_N(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_CMFR.C_bar
one_baffle_CMFR.N
one_baffle_CMFR.theta.to(u.s)

#Create the CMFR model curve based on the scipy.optimize curve_fit
#parameters. We do this with dimensions so that we can plot both models and
#the data on the same graph. If we did this in dimensionless space it wouldn't
#be possible to plot everything on the same plot because the values used to
#create dimensionless time and dimensionless concentration are different for
#the two models.
one_baffle_CMFR_model = (one_baffle_CMFR.C_bar*epa.E_CMFR_N(one_baffle_time_data/one_baffle_CMFR.theta, one_baffle_CMFR.N)).to(u.mg/u.L)

#use solver to get the advection dispersion parameters
one_baffle_AD = epa.Solver_AD_Pe(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_AD.C_bar
one_baffle_AD.Pe
one_baffle_AD.theta

print('The model estimated mass of tracer injected was',ut.round_sf(one_baffle_AD.C_bar*one_baffle_V ,2) )
print('The model estimate of the Peclet number was', one_baffle_AD.Pe)
print('The tracer residence time was',ut.round_sf(one_baffle_AD.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(one_baffle_AD.theta/one_baffle_theta_hydraulic).magnitude)

#Create the advection dispersion model curve based on the solver parameters
one_baffle_AD_model = (one_baffle_AD.C_bar*epa.E_Advective_Dispersion((one_baffle_time_data/one_baffle_AD.theta).to_base_units(), one_baffle_AD.Pe)).to(u.mg/u.L)

#Plot the data and the two model curves.
plt.plot(one_baffle_time_data.to(u.s), one_baffle_concentration_data.to(u.mg/u.L),'ro')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_CMFR_model,'b')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
plt.savefig('C:/Users/dapmo/github/4530/Reactor_24x_5cmholes_sealed_1mldye_1baffle', bbox_inches = 'tight')
plt.show()





M = (10*u.g/u.L).to(u.mg/u.ml)*1*u.ml
#Save CT(in)
E3 = one_baffle_concentration_data*CMFR_V/(M)


tstarvalues=one_baffle_time_data/(ut.round_sf(one_baffle_AD.theta ,2))

F3 = integrate.cumtrapz(E3,tstarvalues)

value = min(F3, key=lambda x:abs(x-.1))

#Calculate Tstar
place = 0
for i in [i for i,x in enumerate(F3) if x == value]:
  place = i
  if place != 0:
   break
tstar=tstarvalues[place]
print('The value for Tstar is',(tstar))




#Load 3nd file

one_baffle_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor2BaffleTest_4x0_5cm.xls'
one_baffle_firstrow = epa.notes(one_baffle_path).last_valid_index() + 1
one_baffle_time_data = (epa.column_of_time(one_baffle_path,one_baffle_firstrow,-1)).to(u.s)
one_baffle_concentration_data = epa.column_of_data(one_baffle_path,one_baffle_firstrow,1,-1,'mg/L')

#I noticed that the initial concentration measured by the photometer wasn't
#zero. This suggests that there may have been a small air bubble in the
#photometer or perhaps there was some other anomoly that was causing the
#photometer to read a concentration that was higher than was actually present in
#the reactor. To correct for this I subtracted the initial concentration reading
#from all of the data. This was based on the assumption that the concentration
#measurement error persisted for the entire experiment.#

one_baffle_concentration_data = one_baffle_concentration_data - one_baffle_concentration_data[0]
one_baffle_V = 2.25*u.L
one_baffle_Q = 380 * u.mL/u.min
one_baffle_theta_hydraulic = (one_baffle_V/one_baffle_Q).to(u.s)
one_baffle_C_bar_guess = np.max(one_baffle_concentration_data)/2
#use solver to get the CMFR parameters
one_baffle_CMFR = epa.Solver_CMFR_N(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_CMFR.C_bar
one_baffle_CMFR.N
one_baffle_CMFR.theta.to(u.s)

#Create the CMFR model curve based on the scipy.optimize curve_fit
#parameters. We do this with dimensions so that we can plot both models and
#the data on the same graph. If we did this in dimensionless space it wouldn't
#be possible to plot everything on the same plot because the values used to
#create dimensionless time and dimensionless concentration are different for
#the two models.
one_baffle_CMFR_model = (one_baffle_CMFR.C_bar*epa.E_CMFR_N(one_baffle_time_data/one_baffle_CMFR.theta, one_baffle_CMFR.N)).to(u.mg/u.L)

#use solver to get the advection dispersion parameters
one_baffle_AD = epa.Solver_AD_Pe(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_AD.C_bar
one_baffle_AD.Pe
one_baffle_AD.theta

print('The model estimated mass of tracer injected was',ut.round_sf(one_baffle_AD.C_bar*one_baffle_V ,2) )
print('The model estimate of the Peclet number was', one_baffle_AD.Pe)
print('The tracer residence time was',ut.round_sf(one_baffle_AD.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(one_baffle_AD.theta/one_baffle_theta_hydraulic).magnitude)

#Create the advection dispersion model curve based on the solver parameters
one_baffle_AD_model = (one_baffle_AD.C_bar*epa.E_Advective_Dispersion((one_baffle_time_data/one_baffle_AD.theta).to_base_units(), one_baffle_AD.Pe)).to(u.mg/u.L)

#Plot the data and the two model curves.
plt.plot(one_baffle_time_data.to(u.s), one_baffle_concentration_data.to(u.mg/u.L),'ro')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_CMFR_model,'b')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
plt.savefig('C:/Users/dapmo/github/4530/Reactor2BaffleTest_4x0_5cm', bbox_inches = 'tight')
plt.show()




M = (10*u.g/u.L).to(u.mg/u.ml)*1*u.ml
#Save CT(in)
E4 = one_baffle_concentration_data*CMFR_V/(M)


tstarvalues=one_baffle_time_data/(ut.round_sf(one_baffle_AD.theta ,2))

F4 = integrate.cumtrapz(E4,tstarvalues)

value = min(F4, key=lambda x:abs(x-.1))

#Calculate Tstar
place = 0
for i in [i for i,x in enumerate(F4) if x == value]:
  place = i
  if place != 0:
   break
tstar=tstarvalues[place]
print('The value for Tstar is',(tstar))









```



Appendix:


from aguaclara.core.units import unit_registry as u
import aguaclara.research.environmental_processes_analysis as epa
import aguaclara.core.utility as ut
import numpy as np
import matplotlib.pyplot as plt
from scipy import integrate

The following file is from a CMFR
CMFR_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor30Test.xls'

 find the row after the last note in the file. This assumes that the last note marks the beginning of the test.
epa.notes(CMFR_path)
CMFR_firstrow = epa.notes(CMFR_path).last_valid_index() + 1
CMFR_firstrow

I eliminate the beginning of the data file because this is a CMFR and the
first data was taken before the dye reached the sensor. Note that eliminating
some data from the beginning of the data file will not change the analysis
except in the estimate of the initial tracer mass.#
CMFR_firstrow = CMFR_firstrow + 10


CMFR_time_data = (epa.column_of_time(CMFR_path,CMFR_firstrow,-1)).to(u.s)

CMFR_concentration_data = epa.column_of_data(CMFR_path,CMFR_firstrow,1,-1,'mg/L')



I don't actually know the values that follow. I'm guessing.
You should use real measured values!#
CMFR_V = 2.25*u.L
CMFR_Q = 380 * u.mL/u.min

here we set estimates that we will use as starting values for the curve fitting
CMFR_theta_hydraulic = (CMFR_V/CMFR_Q).to(u.s)
CMFR_C_bar_guess = np.max(CMFR_concentration_data)

The Solver_CMFR_N will return the initial tracer concentration,
residence time, and number of reactors in series.
This experiment was for a single reactor and so we expect N to be 1!
CMFR_CMFR = epa.Solver_CMFR_N(CMFR_time_data, CMFR_concentration_data, CMFR_theta_hydraulic, CMFR_C_bar_guess)
use dot notation to get the 3 elements of the tuple that are in CMFR.

print('The model estimated mass of tracer injected was',ut.round_sf(CMFR_CMFR.C_bar*CMFR_V ,2) )
print('The model estimate of the number of reactors in series was', CMFR_CMFR.N)
print('The tracer residence time was',ut.round_sf(CMFR_CMFR.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(CMFR_CMFR.theta/CMFR_theta_hydraulic).magnitude)

M = (10*u.g/u.L).to(u.mg/u.ml)*6.75*u.ml
Save CT(in)
E1 = CMFR_concentration_data*CMFR_V/(M)


tstarvalues=CMFR_time_data/(ut.round_sf(CMFR_CMFR.theta ,2))

F1 = integrate.cumtrapz(E1,tstarvalues)

value = min(F1, key=lambda x:abs(x-.1))

Calculate Tstar
place = 0
for i in [i for i,x in enumerate(F1) if x == value]:
  place = i
  if place != 0:
   break
tstarcmfr=tstarvalues[place]
print('The value for Tstar is',(tstarcmfr))


create a model curve given the curve fit parameters.

CMFR_CMFR_model = CMFR_CMFR.C_bar * epa.E_CMFR_N(CMFR_time_data/CMFR_CMFR.theta,CMFR_CMFR.N)
plt.plot(CMFR_time_data.to(u.min), CMFR_concentration_data.to(u.mg/u.L),'ro')
plt.plot(CMFR_time_data.to(u.min), CMFR_CMFR_model,'b')

plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model'])
plt.savefig('C:/Users/dapmo/github/4530/CMFR', bbox_inches = 'tight')
plt.show()

Load a data file for a reactor with baffles.

one_baffle_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor_4x1cmholes_sealed_1mldye_1baffle.xls'
one_baffle_firstrow = epa.notes(one_baffle_path).last_valid_index() + 1
one_baffle_time_data = (epa.column_of_time(one_baffle_path,one_baffle_firstrow,-1)).to(u.s)
one_baffle_concentration_data = epa.column_of_data(one_baffle_path,one_baffle_firstrow,1,-1,'mg/L')


one_baffle_concentration_data = one_baffle_concentration_data - one_baffle_concentration_data[0]
one_baffle_V = 2.25*u.L
one_baffle_Q = 380 * u.mL/u.min
one_baffle_theta_hydraulic = (one_baffle_V/one_baffle_Q).to(u.s)
one_baffle_C_bar_guess = np.max(one_baffle_concentration_data)/2

one_baffle_CMFR = epa.Solver_CMFR_N(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_CMFR.C_bar
one_baffle_CMFR.N
one_baffle_CMFR.theta.to(u.s)

Create the CMFR model curve based on the scipy.optimize curve_fit

one_baffle_CMFR_model = (one_baffle_CMFR.C_bar*epa.E_CMFR_N(one_baffle_time_data/one_baffle_CMFR.theta, one_baffle_CMFR.N)).to(u.mg/u.L)

use solver to get the advection dispersion parameters
one_baffle_AD = epa.Solver_AD_Pe(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_AD.C_bar
one_baffle_AD.Pe
one_baffle_AD.theta

print('The model estimated mass of tracer injected was',ut.round_sf(one_baffle_AD.C_bar*one_baffle_V ,2) )
print('The model estimate of the Peclet number was', one_baffle_AD.Pe)
print('The tracer residence time was',ut.round_sf(one_baffle_AD.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(one_baffle_AD.theta/one_baffle_theta_hydraulic).magnitude)

Create the advection dispersion model curve based on the solver parameters
one_baffle_AD_model = (one_baffle_AD.C_bar*epa.E_Advective_Dispersion((one_baffle_time_data/one_baffle_AD.theta).to_base_units(), one_baffle_AD.Pe)).to(u.mg/u.L)

Plot the data and the two model curves.
plt.plot(one_baffle_time_data.to(u.s), one_baffle_concentration_data.to(u.mg/u.L),'ro')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_CMFR_model,'b')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
plt.savefig('C:/Users/dapmo/github/4530/Reactor_4x1cmholes_sealed_1mldye_1baffle', bbox_inches = 'tight')
plt.show()


M = (10*u.g/u.L).to(u.mg/u.ml)*1*u.ml
Save CT(in)
E2 = one_baffle_concentration_data*CMFR_V/(M)


tstarvalues=one_baffle_time_data/(ut.round_sf(one_baffle_AD.theta ,2))

F2 = integrate.cumtrapz(E2,tstarvalues)

value = min(F2, key=lambda x:abs(x-.1))

Calculate Tstar
place = 0
for i in [i for i,x in enumerate(F2) if x == value]:
  place = i
  if place != 0:
   break
tstar=tstarvalues[place]
print('The value for Tstar is',(tstar))



Load 2nd file

one_baffle_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor_24x_5cmholes_sealed_1mldye_1baffle.xls'
one_baffle_firstrow = epa.notes(one_baffle_path).last_valid_index() + 1
one_baffle_time_data = (epa.column_of_time(one_baffle_path,one_baffle_firstrow,-1)).to(u.s)
one_baffle_concentration_data = epa.column_of_data(one_baffle_path,one_baffle_firstrow,1,-1,'mg/L')

I noticed that the initial concentration measured by the photometer wasn't
zero. This suggests that there may have been a small air bubble in the
photometer or perhaps there was some other anomoly that was causing the
photometer to read a concentration that was higher than was actually present in
the reactor. To correct for this I subtracted the initial concentration reading
from all of the data. This was based on the assumption that the concentration
measurement error persisted for the entire experiment.#

one_baffle_concentration_data = one_baffle_concentration_data - one_baffle_concentration_data[0]
one_baffle_V = 2.25*u.L
one_baffle_Q = 380 * u.mL/u.min
one_baffle_theta_hydraulic = (one_baffle_V/one_baffle_Q).to(u.s)
one_baffle_C_bar_guess = np.max(one_baffle_concentration_data)/2
use solver to get the CMFR parameters
one_baffle_CMFR = epa.Solver_CMFR_N(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_CMFR.C_bar
one_baffle_CMFR.N
one_baffle_CMFR.theta.to(u.s)

Create the CMFR model curve based on the scipy.optimize curve_fit
parameters. We do this with dimensions so that we can plot both models and
the data on the same graph. If we did this in dimensionless space it wouldn't
be possible to plot everything on the same plot because the values used to
create dimensionless time and dimensionless concentration are different for
the two models.
one_baffle_CMFR_model = (one_baffle_CMFR.C_bar*epa.E_CMFR_N(one_baffle_time_data/one_baffle_CMFR.theta, one_baffle_CMFR.N)).to(u.mg/u.L)

use solver to get the advection dispersion parameters
one_baffle_AD = epa.Solver_AD_Pe(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_AD.C_bar
one_baffle_AD.Pe
one_baffle_AD.theta

print('The model estimated mass of tracer injected was',ut.round_sf(one_baffle_AD.C_bar*one_baffle_V ,2) )
print('The model estimate of the Peclet number was', one_baffle_AD.Pe)
print('The tracer residence time was',ut.round_sf(one_baffle_AD.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(one_baffle_AD.theta/one_baffle_theta_hydraulic).magnitude)

Create the advection dispersion model curve based on the solver parameters
one_baffle_AD_model = (one_baffle_AD.C_bar*epa.E_Advective_Dispersion((one_baffle_time_data/one_baffle_AD.theta).to_base_units(), one_baffle_AD.Pe)).to(u.mg/u.L)

Plot the data and the two model curves.
plt.plot(one_baffle_time_data.to(u.s), one_baffle_concentration_data.to(u.mg/u.L),'ro')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_CMFR_model,'b')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
plt.savefig('C:/Users/dapmo/github/4530/Reactor_24x_5cmholes_sealed_1mldye_1baffle', bbox_inches = 'tight')
plt.show()





M = (10*u.g/u.L).to(u.mg/u.ml)*1*u.ml
Save CT(in)
E3 = one_baffle_concentration_data*CMFR_V/(M)


tstarvalues=one_baffle_time_data/(ut.round_sf(one_baffle_AD.theta ,2))

F3 = integrate.cumtrapz(E3,tstarvalues)

value = min(F3, key=lambda x:abs(x-.1))

Calculate Tstar
place = 0
for i in [i for i,x in enumerate(F3) if x == value]:
  place = i
  if place != 0:
   break
tstar=tstarvalues[place]
print('The value for Tstar is',(tstar))




Load 3nd file

one_baffle_path = 'https://raw.githubusercontent.com/DanielPyrek/4530/master/data/Reactor/Reactor2BaffleTest_4x0_5cm.xls'
one_baffle_firstrow = epa.notes(one_baffle_path).last_valid_index() + 1
one_baffle_time_data = (epa.column_of_time(one_baffle_path,one_baffle_firstrow,-1)).to(u.s)
one_baffle_concentration_data = epa.column_of_data(one_baffle_path,one_baffle_firstrow,1,-1,'mg/L')


one_baffle_concentration_data = one_baffle_concentration_data - one_baffle_concentration_data[0]
one_baffle_V = 2.25*u.L
one_baffle_Q = 380 * u.mL/u.min
one_baffle_theta_hydraulic = (one_baffle_V/one_baffle_Q).to(u.s)
one_baffle_C_bar_guess = np.max(one_baffle_concentration_data)/2

one_baffle_CMFR = epa.Solver_CMFR_N(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_CMFR.C_bar
one_baffle_CMFR.N
one_baffle_CMFR.theta.to(u.s)


one_baffle_CMFR_model = (one_baffle_CMFR.C_bar*epa.E_CMFR_N(one_baffle_time_data/one_baffle_CMFR.theta, one_baffle_CMFR.N)).to(u.mg/u.L)


one_baffle_AD = epa.Solver_AD_Pe(one_baffle_time_data, one_baffle_concentration_data, one_baffle_theta_hydraulic, one_baffle_C_bar_guess)
one_baffle_AD.C_bar
one_baffle_AD.Pe
one_baffle_AD.theta

print('The model estimated mass of tracer injected was',ut.round_sf(one_baffle_AD.C_bar*one_baffle_V ,2) )
print('The model estimate of the Peclet number was', one_baffle_AD.Pe)
print('The tracer residence time was',ut.round_sf(one_baffle_AD.theta ,2))
print('The ratio of tracer to hydraulic residence time was',(one_baffle_AD.theta/one_baffle_theta_hydraulic).magnitude)

one_baffle_AD_model = (one_baffle_AD.C_bar*epa.E_Advective_Dispersion((one_baffle_time_data/one_baffle_AD.theta).to_base_units(), one_baffle_AD.Pe)).to(u.mg/u.L)


plt.plot(one_baffle_time_data.to(u.s), one_baffle_concentration_data.to(u.mg/u.L),'ro')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_CMFR_model,'b')
plt.plot(one_baffle_time_data.to(u.s), one_baffle_AD_model,'g')
plt.xlabel(r'$time (min)$')
plt.ylabel(r'Concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(['Measured dye','CMFR Model', 'AD Model'])
plt.savefig('C:/Users/dapmo/github/4530/Reactor2BaffleTest_4x0_5cm', bbox_inches = 'tight')
plt.show()




M = (10*u.g/u.L).to(u.mg/u.ml)*1*u.ml

E4 = one_baffle_concentration_data*CMFR_V/(M)


tstarvalues=one_baffle_time_data/(ut.round_sf(one_baffle_AD.theta ,2))

F4 = integrate.cumtrapz(E4,tstarvalues)

value = min(F4, key=lambda x:abs(x-.1))


place = 0
for i in [i for i,x in enumerate(F4) if x == value]:
  place = i
  if place != 0:
   break
tstar=tstarvalues[place]
print('The value for Tstar is',(tstar))
