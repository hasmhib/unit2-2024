# Quiz 027
<img width="max" alt="Screenshot 2023-12-22 at 11 03 03 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/f3d8782e-1ef8-4729-a129-db73fb8dd938">

## Code

```py
def count_letters(lexicon:dict,msg:str):
    for letter in msg:
        if letter in lexicon:
            lexicon[letter] += 1
    return lexicon

case1 = (count_letters({'w':0,'l':0,'c':0},"hello world"))
print(case1)

case2 = (count_letters({'a':0,'e':0,'i':0,'o':0,'u':0},"Why did I choose CS?"))
print(case2)
```

## Proof of work
<img width="max" alt="Screenshot 2023-12-22 at 11 04 55 AM" src="https://github.com/hasmhib/unit2-2024/assets/142870448/c5eaaf40-b154-477f-893d-bd61a37a0298">

## How many different colors could you represent in a 6 bit computer? 
2^6 = 64
