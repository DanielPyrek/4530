```python

#DanielPyrek and JessiePowell


from aguaclara.core.units import unit_registry as u
import aguaclara.core.physchem as pc

import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from scipy import stats
import numpy



u.define('equivalent = mole = eq')
import aguaclara.research.environmental_processes_analysis as epa





pc.head_orifice(.001,0.63,(6.3333*10**-6)/6)

def f(t):
    return epa.E_Advective_Dispersion(t,1)
def g(b):
    return epa.E_Advective_Dispersion(b,10)
def h(c):
    return epa.E_Advective_Dispersion(c,100)
t1 = np.arange(0.01, 5.0, 0.1)

fig, ax = plt.subplots()

plt.plot(t1, f(t1), 'blue')
plt.plot(t1, g(t1), 'red')
plt.plot(t1, h(t1), 'green')


ax.legend(['Peclet = 1','Peclet = 10','Peclet = 100'])
ax.set(xlabel="t*")
ax.set(ylabel="E(t*)")
ax.grid(True)
plt.savefig('C:/Users/dapmo/github/4530/Prelab5')
plt.show()


```

<b>Prelab Questions</b>
Daniel Daniel
Jessie Powell


<b>Queston 1:</b>
The reactor baffles are perforated with 6 holes 1 mm in diameter. The flow through the orifices are in parallel. The orifices themselves are in series. Using the pc.head_orifice function we found that the head loss is equal to 0.232 meters. We used .00 meters, a ratio of .63, and a flowrate of (6.3333*10^-6)/6 = 0.000001055 m3/s. We do not have to multiply the head loss by six to get the total head loss. Six holes 1mm in diameter might not be a good design for this reactor because a head loss of .23 meters might be too large.

<b>Queston 2:</b>
