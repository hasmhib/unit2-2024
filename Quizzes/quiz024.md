# Quiz 024
<img width="max" alt="Screenshot 2023-11-16 at 11 49 13 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/f9423fee-6a09-4bf8-90ee-7a6167a37422">

## Code

```py
import matplotlib.pyplot as plt
import numpy as np

x = []
h = [57.0, 56.0, 57.0, 56.0, 55.0, 55.0, 54.0, 54.0, 54.0, 53.0, 53.0, 54.0, 53.0, 53.0, 52.0, 52.0, 51.0, 51.0, 51.0, 50.0, 50.0, 49.0, 50.0, 49.0, 49.0, 48.0, 49.0, 49.0, 48.0, 48.0, 48.0, 49.0]
for i in range(1,33):
    x.append(i)

plt.scatter(x, h)
plt.xlabel('Samples')
plt.ylabel('Relative Humidity')
plt.title("Humidity on Campus")

m, b = np.polyfit(x, h, 1)
print(f"Linear equation is y={m:.2f}x+{b:.2f}")
x_model = [1, 33]
h_model = []
for i in x_model:
    h_model.append(m * i + b)
plt.plot(x_model, h_model)
plt.text(6, 50, f"y={m:.2f}x+{b:.2f}")

plt.show()
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 8 04 04 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/c5c0930e-4b74-4653-bf36-ce59cacbab5d">

## Convert the following color in hex to rgb
