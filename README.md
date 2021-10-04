# Memory Leak Manager
This is a simple tool that enables detecting memory leak, the idea is that memory leak occurs when there are some allocations in the heap and there are no references in the stack point to those allocatations.

This tool overloads `new` and `delete` operators to keep track of what is allocated and what is freed.

Due to differences in stack memory management between compilers, this tool detects and collects all memory leaks for GCC and Clang compilers, but for MSVC it can detect and collect all leaks in a function call where `CollectGarbage` function is called after the leaker function context is finished, and if the call of ` CollectGarbage` is in a function where leak took place I distinguish between 2 cases of memory leak, see the testing examples in the MemeoryLeakManager.cpp file.  

# Usage:
- First of all when the program begins or when you still think no leak has been occured the stack top address should be obtained like:
```c++
int dummy = 0;
g_stackTop = &dummy; // g_stackTop is a global variable declared in MemeoryLeakManager.hpp
```
- Somewhere in the program where you think memory leak took place call:
```c++
CollectGarbage();
```
