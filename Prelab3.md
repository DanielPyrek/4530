```python
  from aguaclara.core.units import unit_registry as u
  import numpy as np
  import matplotlib.pyplot as plt
  import pandas as pd
  from scipy import stats

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

  # We can test this function to find the pH of pure water in equilibrium
  # with the atmosphere
  print('The pH of pure water equilibrium with the atmosphere is',.2*3.5+.8*pH_open(1.6*u.meq/u.L))
  phc=.2*3.5+.8*pH_open(1.6*u.meq/u.L)


  print('The pH of pure water equilibrium with the atmosphere is',.2*3.5+.8*pH_open(70*u.ueq/u.L))
  phw=.2*3.5+.8*pH_open(70*u.ueq/u.L)

ANC2=10**(-3.2)*u.eq/u.L
print(ANC2)
  ```
Prelab 3
Daniel Pyrek
Jessie Powell

1 - The pH of cayuga lake is 7.5447 and the ph of wolf pond is 6.4709.

2 - The pH is low enough that we can neglect all concentrations except H+ in the ANC equation. The ANC of a sample of pH 3.2 is:

$$ 10^{\neg3.2}= 0.000631 eq/L$$

3 - Hydrogen ions are generally not conserved because they can react with things in the water like bicarbonate.


  $$ y = 1.794 \times x-3.667  \frac{mg}{L}$$  
