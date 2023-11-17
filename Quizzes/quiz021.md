# Quiz 021
<img width="max" alt="Screenshot 2023-11-16 at 11 46 20 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/e26eb9c2-8039-49d3-afda-ab6195e08fbb">


## Code

```py
from matplotlib import pyplot as plt

import random
random.seed(1234)

def produce(n,m,s):
    out = ""
    random.seed(1234)
    y = []
    x = []
    for i in range(n):
        x_rnd = random.randint(0,100)
        y_rnd = x_rnd**(0.5*((m/s)**2))
        y.append(y_rnd)
        x.append(x_rnd)

    return x,y

y, x = produce(5,3,2)
plt.plot(x,y)
plt.plot(x,y,color="r", marker="o")
plt.title("Graph of the equation $y=x^{-1/2(m/s)^2}$")
plt.xlabel("x",fontsize=18)
plt.ylabel("y",fontsize=18)
plt.show()
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 8 00 51 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/4d605d25-6d1e-4d86-bc6a-ab646e147b58">


## Truth table for
![IMG_0063](https://github.com/hasmhib/unit2-2024/assets/142870448/fc54c1c9-94d3-421b-bee9-de3072b5493c)

