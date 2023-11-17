# Quiz 019
<img width="max" alt="Screenshot 2023-11-16 at 11 42 30 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/731342da-e180-489d-9dcc-76d8f9bfadcb">

## Code

```py
def get_truth():
    print("| A | B | C | AB + not B + not CB |")
    for i in range(8):
        a = i//4
        b = i//2%2
        c = i%2
        d = int(a and b) or int(not b) or int(not b and c)
        print(f"|{str(a).center(3)}|{str(b).center(3)}|{str(c).center(3)}|{str(d).center(21)}|")

table = get_truth()
```

## Proof of work
<img width="max" alt="Screenshot 2023-11-16 at 7 44 17 PM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/f6bde83f-cd32-4aa4-8de1-3e008e3921d8">


## Truth table and circuit
![IMG_0060](https://github.com/hasmhib/unit2-2024/assets/142870448/a490f80e-369a-40ef-aca3-1e09eb83c32b)
![IMG_0061](https://github.com/hasmhib/unit2-2024/assets/142870448/1b9c89c3-f529-4ad9-8b90-10684e6cb0d3)


