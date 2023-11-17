# Quiz 020
<img width="max" alt="Screenshot 2023-11-16 at 11 42 39 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/ca37eadd-446d-4d32-8673-55915cd17d7a">

## Code

```py
import random
random.seed(1234)

def equation(n=int,m=int,s=int):
    print("|  x  |  y(x)  |")
    for i in range(n):
        x = random.randint(0,100)
        y = x ** (1 / 2 * ((m / s) ** 2))
        y_str = f"{y:.2f}"
        print("|" + str(x).center(5) + "|" + y_str.center(8) + "|")

sample = equation(5,3,2)
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 2 56 33 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/0bd37f0d-d7f9-4d90-a196-448eb8097308">

## Proof
![IMG_0062](https://github.com/hasmhib/unit2-2024/assets/142870448/46460a73-d305-4584-ad50-9ba12ff64b0e)

