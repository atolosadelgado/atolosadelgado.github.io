# C++ tricks
----

## Tips when coding

### Private in C++

Private means not public to other classes, but visible among instances of same class. Access control in C++ is meant to work on per-class basis. Check this (link)[https://stackoverflow.com/questions/6921185/why-do-objects-of-the-same-class-have-access-to-each-others-private-data].

### Use forward declaration in headers as much as you can

Check this (link)[https://stackoverflow.com/questions/3962708/how-much-do-forward-declarations-affect-compile-time]

## Tools

### Cloc. Count lines in a file

Use (cloc)[https://www.geeksforgeeks.org/cloc-count-number-of-lines-of-code-in-file/] command.


In linux mint, you may need to install some of the tools,

```shell
sudo apt install clang lldb clang-tools cppcheck clang-tidy valgrind binutils gdb
```

### Profilers

Sampling, perf. Statistical. Do not use gdb for sampling
Instrumentation, adds chronometer to each function: callgrind. Overhead, but precise

Custom made: surround block by TStopWatch (from ROOT) or use these lines to make your own benchmarking

```cpp
If you are using C++11 you can use system_clock::now():

auto start = std::chrono::system_clock::now();

/* do some work */

auto end = std::chrono::system_clock::now();
auto elapsed = end - start;
std::cout << elapsed.count() << '\n';

You can also specify the granularity to use for representing a duration:

// this constructs a duration object using milliseconds
auto elapsed =
    std::chrono::duration_cast<std::chrono::milliseconds>(end - start);

// this constructs a duration object using seconds
auto elapsed =
    std::chrono::duration_cast<std::chrono::seconds>(end - start);

```

#### Valgrind. Memcheck (mem error detector)

Sometimes there is memory invalid access, the program runs but behaviour is not deterministic. By default, if no arguments are passed to valgrind, the option memcheck is run

#### Valgrind. callgrind (profiler)


```cpp
valgrind --tool=callgrind --dump-instr=yes --simulate-cache=yes --collect-jumps=yes ./hello
kcachegrind
```

Important info, left bottom list of times. Difference between total time and self-time (the single instructions inside a function which are not other functions).


see [this web](https://developer.mantidproject.org/ProfilingWithValgrind.html)

#### Valgrind. other tools

See [manual](https://valgrind.org/docs/manual/manual.html) for heap mem profiler, sync and thread error detector, branch and prediction profiler,

#### Gprof


"gprof" produces an execution profile of C, Pascal, or Fortran77
       programs.  The effect of called routines is incorporated in the profile
       of each caller.  The profile data is taken from the call graph profile
       file (gmon.out default) which is created by programs that are compiled
       with the -pg option of "cc", "pc", and "f77".

#### Perf

 Performance analysis tools for Linux


#### cppcheck

Cppcheck is a static analysis tool for C/C++ code. It provides unique code analysis to detect bugs and focuses on detecting undefined behaviour and dangerous coding constructs.
Undefined behaviour
*     Dead pointers
*     Division by zero
*     Integer overflows
*     Invalid bit shift operands
*     Invalid conversions
*     Invalid usage of STL
*     Memory management
*     Null pointer dereferences
*     Out of bounds checking
*     Uninitialized variables
*     Writing const data

#### clang-tidy

see [webpage](https://clang.llvm.org/extra/clang-tidy/).

#### LLVM tools
Clang scan-build, scan-view, are part of LLVM tools.

#### Coverity

CERN has free licenses for Coverity static check. https://coverity.cern.ch/

#### Listing the symbols from object files

Use nm command. Option -C to demangle (show the name of the functions and arguments)

#### Demangling symbols

c++filt id_of_symbol

#### Show libraries that are needed by binary

Use `ldd -r my_binary`

#### GDB

Can be attached to running process.
Basic commands inside GDB: run, where, b file.cpp;9, next,continue,step,

[More info about GDB](https://sourceware.org/gdb/onlinedocs/gdb/Commands.html#Commands)



#### Godbolt

Create machine code in [this web](https://godbolt.org/)

#### cppinsight

https://cppinsights.io/s/b886aa76


## Stories

* Foobar, [according to wikipedia](https://en.wikipedia.org/wiki/Foobar), comes from:

> It is possible that foobar is a playful allusion[2] to the World War II-era military slang FUBAR (Fucked Up Beyond All Recognition).[2]


