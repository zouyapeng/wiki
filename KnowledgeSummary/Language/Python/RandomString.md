###
```python
import random, string

def random_string(length=8):
    all_letters = list(string.ascii_letters+string.digits)
    random_str = []
    for i in range(length):
        index = random.sample(range(0,62), 1)[0]
        random_str = ''.join([random_str, all_letters[index]])
    return random_str
    
    
if __name__ == '__main__':
    print random_string(20)
```