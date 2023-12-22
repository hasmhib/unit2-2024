# Quiz 029
<img width="max" alt="Screenshot 2023-12-22 at 11 26 40 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/3b113dcc-5d7d-4184-bdb3-74333533f28b">

## Code

```py
def sort_dict_mixed(in_dict):

    sorted_dict = {}
    temp_dict = {}
    for k, v in in_dict.items():
        if isinstance(v, (int, float)):
            temp_dict[k] = v
        else:
            sorted_dict[k] = v

    # Sort items with numerical values and update the sorted_dict with them
    sorted_items = sorted(temp_dict.items(), key=lambda item: item[1])
    sorted_dict.update(sorted_items)
    return sorted_dict


test1 = {'apple': 'red', 'banana': 2, 'orange': 'orange', 'grape': 1, 'kiwi': 'brown', 'pear': 8}
case1 = sort_dict_mixed(test1)
print(case1)
```

## Proof of work
<img width="max" alt="Screenshot 2023-12-22 at 11 29 34 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/e063aad5-9d59-4867-8c90-73e38038f217">

## Code for y=sin(2*pi*x) 0<x<1

```.py
import numpy as np
import matplotlib.pyplot as plt

x_values = np.linspace(0, 1, 500)
y_values = np.sin(2 * np.pi * x_values)

plt.plot(x_values, y_values)
plt.title('Graph of y = sin(2*pi*x)')
plt.xlabel('x')
plt.ylabel('y')
plt.grid(True)
plt.show()
```
## Proof of work for y=sin(2*pi*x) 0<x<1
<img width="max" alt="Screenshot 2023-12-22 at 11 31 07 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/c045ad7f-c6f6-4e45-9f87-04d1ce3c3d65">





