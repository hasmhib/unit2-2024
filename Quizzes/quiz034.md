# Quiz034
<img width="max" alt="Screenshot 2023-12-22 at 11 40 50 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/f9fd6290-ac90-4298-936c-9f855528b6d1">

## Code
```.py
import matplotlib.pyplot as plt
import numpy as np

x1 = np.linspace(-15, 0, 1000)
x2 = np.linspace(0, 15, 1000)
x3 = np.linspace(-15, 0, 1000)
x4 = np.linspace(0, 15, 1000)

y1 = (x1 + 2)**2
y2 = (x2 - 2)**2
y3 = -((x3 + 2)**2)
y4 = -((x4 - 2)**2)

plt.figure(figsize=(6, 6))
plt.plot(x1, y1, 'r', label='Parabola 1: $(x+2)^2$')
plt.plot(x2, y2, 'b', label='Parabola 2: $(x-2)^2$')
plt.plot(x3, y3, 'purple', label='Parabola 3: $-(x+2)^2$')
plt.plot(x4, y4, 'grey', label='Parabola 4: $-(x-2)^2$')

plt.xlabel('X-axis')
plt.ylabel('Y-axis')
plt.title('Four Funny Parabolas')
plt.legend()
plt.grid(True)
plt.xlim(-15, 15)
plt.ylim(-15, 15)
plt.show()

```

## Proof of work
<img width="max" alt="Screenshot 2023-12-22 at 0 39 53 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/1bc9f757-2636-4f02-be1d-a6f49d324a69">


