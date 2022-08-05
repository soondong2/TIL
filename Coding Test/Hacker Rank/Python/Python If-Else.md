# 2022/08/05 Fri

# Python If-Else

## 문제
**Task**
Given an integer, , perform the following conditional actions:

If **n** is odd, print Weird
If **n** is even and in the inclusive range of **2** to **5**, print Not Weird
If **n** is even and in the inclusive range of **6** to **20**, print Weird
If **n** is even and greater than **20**, print Not Weird

<br>

**Input Format**

A single line containing a positive integer, **n**.

**Output Format**

Print Weird if the number is weird. Otherwise, print Not Weird.

**Sample Input 0**

3

**Sample Output 0**

Weird

## 풀이
```python
#!/bin/python3

import math
import os
import random
import re
import sys



if __name__ == '__main__':
    n = int(input().strip())
    if n % 2 != 0:
        print('Weird')
    elif (n >= 2) & (n <= 5):
        print('Not Weird')
    elif (n >= 6) & (n <= 20):
        print('Weird')
    elif n > 20:
        print('Not Weird')
```
