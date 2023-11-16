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

y, x = produce(10,3,2)
plt.plot(x,y)
plt.plot(x,y,color="r", marker="o")
plt.title("Graph of the equation $y=x^{-1/2(m/s)^2}$")
plt.xlabel("x",fontsize=18)
plt.ylabel("y",fontsize=18)
plt.show()
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 7 55 26 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/6c8f19c0-1e0c-46bf-a467-4ad60607ef83">

## Truth table for
