# Quiz 022
<img width="max" alt="Screenshot 2023-11-16 at 11 46 53 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/ec778b68-ca93-43b6-b9ea-eeebeff49a0b">


## Code

```py
from matplotlib import pyplot as plt

def equation():
    x_list = []
    y_list = []
    for i in range(-10,10):
        x = -10+i*0.2
        x_list.append(x)
        y = 2*(i+5)**2
        y_list.append(y)
    return y_list,x_list

data_y,data_x = equation()

plt.plot(data_x, data_y, color="r")
plt.xlabel("x")
plt.ylabel("$y=2(x+5)^2$")
plt.show()
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 8 01 48 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/4c4dd971-9bcb-4ba0-9d19-1e6f1cd51e77">

## Circuit for
![IMG_0064](https://github.com/hasmhib/unit2-2024/assets/142870448/4b5cd2d6-f69b-4667-adef-0737a30d7b7e)
