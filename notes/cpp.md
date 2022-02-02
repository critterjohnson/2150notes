---
slug: "/notes/cpp"
date: "2022-01-22"
title: "C++"
---

# C++

## Operators and Expressions
- inside of an if statement can be an int

    ```cpp
    if ( x = 0 ) // perfectly valid
    ```

## Single-pass compiler
- as opposed to multi-pass compiler
- mutually recursive functions won't work unless you define a function prototype
        - called a forward declaration in this context

    ```cpp
    bool even (int x); // forward declaration
    ```

## Classes

- in C++, variables of objects are not refs, they are the objects themselves

    `IntCell.cpp`

    ```cpp
    #include <iostream>
    #include "IntCell.h"
    using namespace std;

    int main() {
        IntCell m1; // calls default constructor
        IntCell m2(37);

        m1 = m2;
        m2.setValue(40); // still separate objects, just now m2's value is the same as m1
    }
    ```

    `IntCell.h`

    ```cpp
    #ifndef INTCELL_H // every .h needs to start with these
    #define INTCELL_H

    class IntCell {
        public:
                IntCell(int initialValue = 0);

                int getValue() const; // const means won't modify obj
                void setValue(int val);

        private:
                int storedValue;
                int max(int m) const;
    }

    #endif // every .h needs to end with this
    ```

    ```cpp
    #include "IntCell.h"
    using namespace std;

    IntCell::IntCell(int initialValue) :
        storedValue(initialValue) {
    } // this syntax only allowed in constructors

    int IntCell::getValue() const {
        return storedValue;
    }

    void IntCell::setValue(int val) {
        storedValue = val;
    }

    int IntCell::max(int m) const {
        return (m > storedValue) ? m : storedValue; // this
    }
    ```

- destructors defined with a `~` in front of the class name, no params

## Preprocessing

- `#include` - directly copies file to the location specified, only do this for
    .h files
- `#ifndef` - if not defined (also `#ifdef`, `#if`)
- `#endif` - end of an `#if`
- `#define` - defines a macro (direct text replacement)

## Memory

- anything allocated with `new` is on the heap
  - must be deallocated with `delete`
- when accessing a field of the pointer's pointee, have to deref
  ```cpp
  // these are equivalent
  (*r).num = 4;
  r->num = 4;
  ```

## Defaults

- C++ provides some defaults - but they have some issues
  - constructor
  - copy constructor
    ```cpp
    IntCell original;
    IntCell copy = original // or copy(original)
    ```
  - destructor
  - operator=()
    ```cpp
    IntCell original; // constructor called
    IntCell copy;
    copy = original; // operator= called
    ```
    - called when `=` is applied to two objects *after* both have previously
        been constructed

## STL

- `vector` - better array, can be copied and items can be found within it
  - doubles its internal array in size when it gets full and copies everything
      to the new one
- `string` - better C string
