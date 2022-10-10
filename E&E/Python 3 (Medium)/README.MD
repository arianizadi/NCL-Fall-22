# Python Script Authentication

## Validation Code Given

Given is a python PYC file, which is a compiled python file. We can decompile it using uncompyle6.

```bash
uncompyle6 PYTHON3.pyc
```

```Python
# uncompyle6 version 3.8.0
# Python bytecode 2.7 (62211)
# Decompiled from: Python 3.8.10 (default, Jun 22 2022, 20:18:18)
# [GCC 9.4.0]
# Embedded file name: NCL-2015-Python3.py
# Compiled at: 2015-11-12 17:09:05
import sys

def main():
    if len(sys.argv) != 2:
        print 'Invalid args'
        return
    password = sys.argv[1]
    builder = 0
    for c in password:
        builder += ord(c)

    builder = builder << 2
    builder = ~builder
    builder = builder ^ 12648430
    builder = ~builder
    if builder == 12645638 and ord(password[0]) == 78 and len(password) == 11:
        print 'correct'
    else:
        print 'incorrect'


if __name__ == '__main__':
    main()
# okay decompiling PYTHON3.pyc
```

Looking at this decompiled code, we can see that the password is validated by a series of bitwise operations. It is good to know the calculations being done, but the main thing is to note the order of operations and then reverse it to solve for the flag.

```Python
>>> b = 12645638
>>> b = ~b
>>> b = b ^ 12648430
>>> b = ~b
>>> b = b >> 2
>>> b
698
>>> b = b - 78
>>> chr(78)
'N'
>>> 620 / 10
62.0
>>> chr(62)
'>'
```

Using this we can figure out that the flag is **`N>>>>>>>>>>`**
