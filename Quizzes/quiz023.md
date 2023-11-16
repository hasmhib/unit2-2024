# Quiz 023
<img width="max" alt="Screenshot 2023-11-16 at 11 47 36 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/f190f5d4-60de-4d7a-b5e0-1993b8969c70">

## Code

```py
def produce():
    st = -10
    len=10
    x = []
    y = []
    for i in range(101):
        x.append(st)
        y_out = abs(st)
        y.append(y_out)
        st += 0.2
    return x, y

data_x, data_y = produce()
from matplotlib import pyplot as plt
plt.plot(data_x, data_y, color="red", marker= '.')
plt.ylabel("$f(x)=|x|$")
plt.show()
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 2 53 00 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/a227a815-f74a-49fb-9cb6-a69378de74a8">

## Convert to decimal

