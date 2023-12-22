# Quiz 028

<img width="max" alt="Screenshot 2023-12-22 at 11 07 51 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/337f1873-ef71-4ffc-b81e-ec8442341b69">

## Code for SL and HL

```py
def in_dict(input_dict):
    inverted_dict = {}
    for key, value in input_dict.items():
        if value in inverted_dict:
            inverted_dict[value].append(key)
        else:
            inverted_dict[value] = [key]

    for key in inverted_dict:
        if len(inverted_dict[key]) == 1:
            inverted_dict[key] = inverted_dict[key][0]
    return inverted_dict

test1 = {'a': 1, 'b': 2, 'c': 3}
case1 = in_dict(test1)

print(case1)
```

## Proof of work for SL
<img width="max" alt="Screenshot 2023-12-22 at 11 13 17 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/648bb4fd-3b1f-4493-9c96-5d9aac285e50">

## Proof of work for HL
<img width="max" alt="Screenshot 2023-12-22 at 11 15 05 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/5e04493b-5905-4d43-a43d-2015b059190f">


## Add the binary numbers 1011 and 1101 and express the result in binary

The sum of the binary numbers 1011 and 1101 is 11000 (Binary)




