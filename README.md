# Run-c-funtion-with-python
An explanation for how to run c function from python script

## Convert .c to .os 
In oreder to run funtion that was written in C we must conver the source code to __.so__ (shared object)  file.
Its can be done by using command line:
```
gcc -m32 -shared -o libhello.so -fPIC hello.c
```
or can be done in python by:
```Python
import os
os.popen("gcc -m32 -shared -o libhello.so -fPIC hello.c").close()
```
If you see the next warrning you can simple ignore that `warning: -fPIC ignored for target (all code is position independent)`

## Usage

### This is our C code:
```C
#include <stdio.h>
long factorial(int user_input) 
{
  long return_val = 1;
  if (user_input <= 0) {
    return -1; }
  else {
    for (long i = 1; i <= user_input; i++) {
      return_val *= i;
    }
  }
  return return_val;
}

int main() { 

    return 0;
}
```
### This is the python code
```python
from ctypes import *
cfactorial = CDLL(r"..Path\libhello.so")
def factorial(num):
  c_return = cfactorial.factorial(num)
  if (c_return != -1):
    return c_return
  else:
    return "C Function failed"
```



