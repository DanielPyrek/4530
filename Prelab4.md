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


  ```
Prelab 4
Daniel Pyrek
Jessie Powell

#1
$$\frac{{mole\; O}_{{2}} }{{32000\; mg\; O}_{{2}} } \cdot \frac{{2\; mole\; Na}_{{2}} {SO}_{{3}} }{{mole\; O}_{{2}} } \cdot \frac{{126,000\; mg\; Na}_{{2}} {SO}_{{3}} }{{mole\; Na}_{{2}} {SO}_{{3}} } =\frac{{\; 7.875\; mg\; Na}_{{2}} {SO}_{{3}} }{{mg\; O}_{{2}} }$$


$$.75L \cdot 10 \frac{mg}{L} \;O_{{2}} = 7.5 mg \:O_{{2}}$$

$$\frac{{\; 7.875\; mg\; Na}_{{2}} {SO}_{{3}} }{{mg\; O}_{{2}}} \cdot 7.5 mg \:O_{{2}} = 59.0625 mg \:Na_{{2}} {SO}_{{3}}  $$

#2
The graph would start a concentration of zero oxygen. Then it would quickly increase and then level off. Therefore it would look logarithmic.

#3
Even when there is no oxygen pumping into the lake, oxygen can still diffuse into the water via the surface in contact with the atmosphere.

#4
The volumetric gas transfer coefficient will start out high as oxygen levels are zero, and then logarithmicly decrease to zero. It would theoretically take an infinite k value to keep the lake at saturation levels.

#5

$$4e^{-} + 4H^{+} + O_{2} \rightarrow 2H_{2}O $$

The DO probe is conducting the reaction above. Therefore, eventually all oxygen will be reduced into water, and there will be no oxygen left.
