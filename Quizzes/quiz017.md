# Quiz 017
<img width="max" alt="Screenshot 2023-11-16 at 11 41 54 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/004226b3-807e-4994-b3ce-831edd870460">

## Code

```py
def get_l3tt3r(msg=str):
    message =" "
    vowels = ["a","e","i","o", " "]
    numbers = ["4","3","1","0","_"]
    for letter in msg:
        if letter in vowels:
            v = vowels.index(letter)
            message += numbers[v]

        else:
            message += letter
    return message

case1 = get_l3tt3r("Hello World")
print(case1)
case1 = get_l3tt3r("Why did I choose CS?")
print(case1)
case1 = get_l3tt3r("Remember the Figure Caption")
print(case1)
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 2 56 38 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/a8b90ddf-9659-45fa-be4a-b5032da8820c">

