# Quiz 033
<img width="max" alt="Screenshot 2023-12-22 at 11 36 01 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/8ad86021-998b-4f81-8274-48f589d19095">

## Code

```py
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-4, 4, 400)
y1 = x**2
y2 = -(x**2)
x1 = y1
x2 = y2

plt.figure(figsize=(6, 6))
plt.plot(x, y1, label='Parabola 1 (x-axis)', color='red')
plt.plot(x, y2, label='Parabola 2 (x-axis)', color='blue')
plt.plot(x1, x, label='Parabola 3 (y-axis)', color='orange')
plt.plot(x2, x, label='Parabola 4 (y-axis)', color='purple')

plt.title('Four Parabolas Aligned with Axes')
plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.legend()
plt.grid(True)
plt.axhline(0, color='black', linewidth=0.5)
plt.axvline(0, color='black', linewidth=0.5)
plt.xlim(-4, 4)
plt.ylim(-4, 4)
plt.show()

```

## Proof of work
<img width="max" alt="Screenshot 2023-12-22 at 11 39 25 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/17c21af1-ee6b-408a-b158-0c0f06266fbc">




