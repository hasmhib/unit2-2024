# Quiz 025
<img width="max" alt="Screenshot 2023-11-16 at 0 00 15 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/e69e2a66-5b2c-454e-b887-27e4509db412">

## Code

```py
import matplotlib.pyplot as plt
import numpy as np

sensorA = [16, 24, 24, 9, 23, 26, 26, 23, 25, 14]
sensorB = [2, 19, 25, 10, 11, 24, 17, 7, 24, 17]
sensorC = [15, 11, 24, 21, 6, 2, 18, 27, 1, 16]

temp = list(range(1, len(sensorA) + 1))  # Create a list of x-values
mean = []
standard_dev = []
max_t = []
min_t = []

for i in range(len(sensorA)):
    data = [sensorA[i], sensorB[i], sensorC[i]]
    mean.append(np.mean(data))
    standard_dev.append(np.std(data))
    max_t.append(max(data))
    min_t.append(min(data))

print(mean)
print(standard_dev)
print(max_t)
print(min_t)
print(temp)

plt.fill_between(temp, max_t, min_t, alpha=0.5, linewidth=0, color="#8ecae6")
plt.errorbar(temp, mean, standard_dev, fmt="o")
plt.show()
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-17 at 1 22 42 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/7b3b698a-f00a-4cda-ae7d-6ef76f222eda">

## Convert the following rgb color to hex color 



