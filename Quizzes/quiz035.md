# Quiz 035

## Code

```.py
import matplotlib.pyplot as plt
import numpy as np

x1_codes = np.arange(-2, 2, 0.01)
x2_codes = np.arange(-2, 2, 0.01)
x3_codes = np.linspace(-1, 1, 100)

y1_values = [-2 * x1 - 1 for x1 in x1_codes]
y2_values = [2 * x2 - 1 for x2 in x2_codes]
y3_values = [-(x**2) + 2 for x in x3_codes]

plt.plot(x1_codes, y1_values, color="Red")
plt.plot(x2_codes, y2_values, color="blue")
plt.plot(x3_codes, y3_values, color="green")

plt.xlim(-1, 1)
plt.ylim(-1, 2)

plt.grid(True)
plt.show()
```

## Proof of work
<img width="max" alt="Screenshot 2023-12-22 at 0 43 43 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/cb5eefad-15c9-4e5c-a7ed-3ce1492b142d">

