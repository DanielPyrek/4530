**Adsorption Prelab**
**Group 8**
3/20/19
Daniel Pyrek - 1 hours
Jessie Powell - 1 hours

A carbon column is packed with 15 cm of activated carbon and then used to remove 50 mg/L of red dye #40. The approach velocity is 1 mm/s, the porosity is 0.4, and the bulk density of the activated carbon is 0.5 g/cm3. How long will it take for the mass transfer zone to travel to the bottom of the carbon column?

$$\frac{L_{column}}{v_{mtz}} = \frac{L_{column}\phi}{v_a} + \frac{L_{column}q_0 \rho_{bulk \; adsorbent}}{v_a C_0}$$

is equivalent to:

$$t_{mtz} = t_{water} + t_{ads}$$

therefore

$$t_{mtz} = \frac{L_{column}\phi}{v_a} + \frac{L_{column}q_0 \rho_{bulk \; adsorbent}}{v_a C_0}$$:

where
Va = 1*mm/second
porosity = .4
L = 15 cm
q = 0.08
bulk = .5 g/cm^3
Co = 50 mg/L

Plugging in and converting units gives:

$$t_{mtz} = 33.35 hrs $$

Therefore 33.35 hours are needed for the mass transfer to reach the bottom.


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

Va = (1*u.mm/u.second).to(u.cm/u.s)
porosity = 0.4
L = 15*u.cm
q = 0.08
bulk = (.5 *u.g/(u.cm)**3).to(u.mg/u.cm**3)
Co = (50*u.mg/u.L).to(u.mg/u.cm**3)
tmtz = (L*porosity/Va)+(L*q*bulk/Va/Co)
tmtz = tmtz.to(u.hours)
print(tmtz)
```
