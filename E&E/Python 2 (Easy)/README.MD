# Python Script Authentication

## What is a PYC file?

It is a compiled version of a Python script. When it is compiled, it is converted into bytecode. You can test this by opening a PYC file in a text editor. You will see a bunch of random characters. This is because the PYC file is not human readable.

## Can we decompile a PYC file?

Yes, we can decompile a PYC file. There are many tools available for this. One of them is uncompyle6. You can install it using the following command:

```bash
pip install uncompyle6
```

## How to use uncompyle6?

```bash
uncompyle6 <filename>.pyc
```

## Decompiled Script

```Python
# uncompyle6 version 3.8.0
# Python bytecode 2.7 (62211)
# Decompiled from: Python 3.8.10 (default, Jun 22 2022, 20:18:18)
# [GCC 9.4.0]
# Embedded file name: NCL-2015-Python2.py
# Compiled at: 2015-11-12 14:43:01
import sys

def main():
    if len(sys.argv) != 2:
        print 'Invalid args'
        return
    password = sys.argv[1]
    counter = 0
    vals = list('tfzbwlyzljylawhzzdvyk')
    if len(password) != len(vals):
        print 'incorrect'
        return
    while counter < len(password):
        x = ord(password[counter]) + 7
        if x > ord('z'):
            x -= 26
        if chr(x) != vals[counter]:
            print 'incorrect'
            return
        counter += 1

    print 'correct'


if __name__ == '__main__':
    main()
# okay decompiling PYTHON2.pyc
```

## How to solve

1. The flag must be the same length as the list of characters.
2. Each character of the flag is shifted by +7 to equal the character in the list.
3. To decode you must shift the final list by -7 to get the flag.

## Ceaser Cipher

A type of substitution cipher in which each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.

> I used [CyberChef](https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,false,-7)&input=dGZ6YndseXpsanlsYXdoenpkdnlr) to decode the flag.

The decoded flag is: **`mysupersecretpassword`**.
