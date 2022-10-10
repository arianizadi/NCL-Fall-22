# Python Script Authentication

## Validation Code Given

```Python
#!/usr/bin/python

import sys

def main():
  if len(sys.argv) != 2:
    print("Invalid args")
    return
  password = sys.argv[1]
  builder = 0
  for c in password:
    builder += ord(c)
  if builder == 1000 and len(password) == 10 and ord(password[1]) == 83:
    print("correct")
  else:
    print("incorrect")

if __name__ == "__main__":
  main()
```

## Identify Common Code

```Python
#!/usr/bin/python
```

Python is being used.

```Python
if len(sys.argv) != 2:
  print("Invalid args")
  return
password = sys.argv[1]
```

Argument passed will be given to password variable

```Python
builder = 0
for c in password:
  builder += ord(c)
```

Looping through each character in the password string.

ord() function return the unicode value for the character.

Adding the unicode value to the builder variable.

```Python
if builder == 1000 and len(password) == 10 and ord(password[1]) == 83:
  print("correct")
else:
  print("incorrect")
```

1. Checking if the builder variable is equal to 1000.

2. Checking if the length of the password is equal to 10.

3. Checking if the unicode value of the second character in the password is equal to 83.

## Step 1 - Easy Finds

1. The password must be 10 characters long.

2. Identify the character with the unicode value of 83.

```Python
>>> chr(83)
'S'
```

The character is S. This will be in position 1 of the password. (0 based index)

## Step 2 - Builder Variable

We know that the builder variable must be equal to 1000 after the loop is done. We also know that the ord() function returns the unicode value of the character. We can use this to our advantage. Although brute force is possible we can use simple math to find the password.

Subtract the value we know in position 1 from 1000.

## 1000 - 83 = 917

Then we know there are 9 more characters left in the password. We can divide the remaining value by 9 to find the unicode value of each character.

## 917 / 9 = 101.889

We can round this down to 100 to make it easier to find the last character.

## 100 * 8 = 800

We know the unicode value of the second character is 83. We can subtract this from the remaining value to find the unicode value of the last character.

## 1000 - 83 - 800 = 117

We can now use the chr() function to find the final character.

```Python
>>> chr(100)
'd'

>>> chr(117)
'u'
```

## Step 3 - The Flag

We now know the password is 10 characters long and the second character is S.

Fill in the rest of the password with the characters we found in the previous step. The flag is **`dSdddddddu`**.
