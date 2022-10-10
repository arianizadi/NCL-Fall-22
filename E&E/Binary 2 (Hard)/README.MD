# Binary Reversing

## Given Information

Given a binary file and a identifier of 4930 that must be passed to the binary when running it.

## File Analysis

As we are getting more experience with reverse I can skip some of the steps that we did in the previous challenges. First, I ran the binary to look for strings and other functionalities so I can get a better understanding of what the binary does.

Opening the file in IDA we can see there a function list being displayed on the left side of the screen. We can see that there are 2 functions that are interesting to us, main and getflagbytid.

```c
// Main Decompiled
int __cdecl main(int argc, const char **argv, const char **envp)
{
  char v4[60]; // [rsp+10h] [rbp-40h] BYREF
  int v5; // [rsp+4Ch] [rbp-4h]

  if ( argc != 2 )
  {
    printf("usage: %s <tid>\n", *argv);
    exit(1);
  }
  if ( strlen(argv[1]) != 4 )
  {
    printf("usage: %s <tid>\n", *argv);
    exit(1);
  }
  v5 = strtol(argv[1], 0LL, 10);
  printf("Please enter a password: ");
  __isoc99_scanf("%s", v4);
  printf("Getting the flag from the program.");
  fflush(_bss_start);
  sleep(1u);
  putchar('.');
  fflush(_bss_start);
  sleep(1u);
  putchar('.');
  fflush(_bss_start);
  sleep(1u);
  putchar('.');
  fflush(_bss_start);
  sleep(1u);
  puts(" password incorrect");
  return 0;
}
```

Looking at the main function we can see that it is using a function called _fflush. This is used to flush the output buffer of a stream. It is not really important as we just want to find the flag. Unfortuntely, the function getflagbytid is not being called at all.

Let us open the function and figure out what is going on. Generating the pseudocode we can see it is utilizing the same techniques as the last challenge, except shortened into one printf statement.

```c
// Getflagbytid Decompiled
int __fastcall getflagbytid(int a1)
{
  char s[16]; // [rsp+10h] [rbp-10h] BYREF

  memset(s, 0, 0xEuLL);
  qmemcpy(s, "NCL-FYOF-", 9);
  return printf(
           "%s%c%c%c%c\n",
           s,
           (unsigned int)cs_2856[(a1 + 140) % 10 + 52],
           (unsigned int)cs_2856[(a1 - 5200) % 9 + 52],
           (unsigned int)cs_2856[(10 * a1 - 120) % 8 + 52],
           (unsigned int)cs_2856[(a1 + 9200) % 7 + 52]);
}
```

Convering this into c++ code for us to run and capture the output so that we can view the flag.

```c++
#include <iostream>

using namespace std;

int main() {
  char str[] = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
  char s[] = "NCL-FYOF-";

  printf("%s%c%c%c%c\n", s, str[(4930 + 140) % 10 + 52],
         str[(4930 - 5200) % 9 + 52], str[(10 * 4930 - 120) % 8 + 52],
         str[(4930 + 9200) % 7 + 52]);
}
```

Running the program we get the flag.

```bash
$ ./getFlag
NCL-FYOF-0044
```
