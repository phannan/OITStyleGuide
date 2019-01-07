# C++ Coding Standards for CST116 / CST126 / CST136

If you are in 116 or 126 there will be new stuff that you don't understand.  That is ok.  If we haven't covered it yet, then ignore it.

Check back for new versions before you start each lab.

These standards started life here:  https://gist.github.com/lefticus/10191322#file-codingstandards-1-style-md  I've heavily modified.  Any weirdness is mine and goodness is probably from the source.

## Site your source
When you didn't originate the code, site your source.  For example see above.

## Don't Pause at the end
* Don't do a getch() at the end of your program.  It is depricated.
* Don't use other methods for keeping your console app on the screen.  Instead use Ctrl-F5 to run or add breakpoints.

## auto
* Ask permission before using auto.  You will need to convince the instructor that you understand the pros and cons of your choice.

## Check your spelling and grammar on your output
* The user will turn on the bozo bit if you leave in spelling or grammatical errors.  Copy your output into a word docuiment if you need to.

## Descriptive and Consistent Naming

C++ allows for arbitrary length identifier names, so there's no reason to be terse when naming variables. Use descriptive names, and be consistent in the style

 * `CamelCase` or `camelCase`
 * `snake_case`
 
are common examples. snake_case has the advantage that it can also work with spell checkers, if desired.

Chose either 'CamelCase' or snake_case and stick to it within your program.  

### Common C++ Naming Conventions

 * Constants are all capital: `const int PI=3.14159265358979323;`
 * Prefer a verb_noun or VerbNoun name for functions.  Once you chose a scheme stick to it throughout the program. For class methods the noun can be implied.
 * Prefer nouns for data names.  
 
 * Name your variable something meaningful.  i, j, k are fine for loop variables.  Otherwise single letter variable names aren't helpful and will confuse you and your reader.  
     * The reader should understand what the variable / method / constant does using the name only.
     * Avoid doh! comments and name your variables well.  
 
 Note:  Many people also prefer to have standard capitalization for functions and classes ie:
 * Types start with capitals: `MyClass`
 * Functions and variables start with lower case: `myMethod`
 
 I never remember this, so I won't require it of you.

*Note that the C++ standard does not follow any of these guidelines. Everything in the standard is lowercase only.*






### Unstructured Jumping
+ If *goto's* you use, cranky instructor you will make.  Many points will you lose.  
+ In 116,126, 136 we will only use *break* statements connected to a switch statement.  There are situations where it is reasonable to use breaks and in these classes we wont.  You may only use them if you can make a cogent arugument for a break and you get permision _in advance_.
+ In 116,126, 136 we will not use *continue* statements.   There are situations where it is reasonable to use continue statements and in these classes we wont.  You may only use them if you can make a cogent arugument and you get permision _in advance_.

### Distinguish Private Object Data

Name private data with a prefix to distinguish it from public data.  I prefer:  `m_`  and you can use _ instead.

Please do this.  It will drive you and your instructor nuts otherwise.


### Well formed example

```cpp
class MyClass
{
public:
  MyClass(int t_data)
    : m_data(t_data)
  {
  }
  
  int getData() const
  {
    return m_data;
  }
  
private:
  int m_data;
};
```

## Use `nullptr`

C++11 introduces `nullptr` which is a special type denoting a null pointer value. This should be used instead of 0 or NULL to indicate a null pointer.

## Comments

Comment blocks should use `//`, not `/* */`. Using `//` makes it much easier to comment out a block of code while debugging.

Its ok to comment out code.  You also can use #ifdef TODO to block out code you aren't finished with yet.  

It is better to turn an incomplete program that is compiling and has commented out code then an aborting or not compiling program.

## Include Guards

Header files must contain an distinctly named include guard to avoid problems with including the same header multiple times or conflicting with other headers from other projects

```cpp
#ifndef MYPROJECT_MYCLASS_H
#define MYPROEJCT_MYCLASS_H

namespace MyProject {
class MyClass {
};
}

#endif
```
You can also use *#pragma once*  IF and Only IF you explain it the first time you use it. 

## Includes and Namespaces
*  Only include libraries you need.  Including extra libraries = bloat.  If you can comment it out and it still compiles, it doesn't belong.
* CST136 programs should have using std::<the thing you are using>.  CST116 & CST126 can use "using namespace std". 
* Never Use `using` In a Header File.  This causes the name space you are `using` to be pulled into the namespace of the header file.
 
## Use consistent indenting. 

Tabs are not allowed, and a mixture of tabs and spaces is strictly forbidden. Modern autoindenting IDEs and editors require a consistent standard to be set.

```cpp
// Good Idea
int myFunction(bool t_b)
{
  if (t_b)
  {
    // do something
  }
}
```

## {} are required for blocks. 
Leaving them off can lead to semantic errors in the code.

```cpp
// Bad Idea
// the cout is not part of the loop in this case even though it appears to be
int sum = 0;
for (int i = 0; i < 15; ++i)
  ++sum;
  std::cout << i << std::endl;
  
  
// Good Idea
// It's clear which statements are part of the loop (or if block, or whatever)
int sum = 0;
for (int i = 0; i < 15; ++i) {
  ++sum;
  std::cout << i << std::endl;
}
```

## Keep lines a reasonable length

```cpp
// Bad Idea
// hard to follow
if (x && y && myFunctionThatReturnsBool() && caseNumber3 && (15 > 12 || 2 < 3)) { 
}

// Good Idea
// Logical grouping, easier to read
if (x && y && myFunctionThatReturnsBool() 
    && caseNumber3 
    && (15 > 12 || 2 < 3)) { 
}
```


## Use "" For Including Local Files
... `<>` is [reserved for system includes](http://blog2.emptycrate.com/content/when-use-include-verses-include).

```cpp
// Bad Idea. Requires extra -I directives to the compiler
// and goes against standards
#include <string>
#include <includes/MyHeader.h>

// Worse Idea
// requires potentially even more specific -I directives and 
// makes code more difficult to package and distribute
#include <string>
#include <MyHeader.h>


// Good Idea
// requires no extra params and notifies the user that the file
// is a local file
#include <string>
#include "MyHeader.h"
```

## Initialize Member Variables
...with the member initializer list

```cpp
// Bad Idea
class MyClass
{
public:
  MyClass(int t_value)
  {
    m_value = t_value;
  }

private:
  int m_value;
};


// Good Idea
// C++'s member initializer list is unique to the language and leads to
// cleaner code and potential performance gains that other languages cannot 
// match
class MyClass
{
public:
  MyClass(int t_value)
    : m_value(t_value)
  {
  }

private:
  int m_value;
};
```

## Forward Declare when Possible

This:
```cpp
// some header file
class MyClass;

void doSomething(const MyClass &);
```

instead of:

```cpp
// some header file
#include "MyClass.h"

void doSomething(const MyClass &);
```

This is a proactive approach to simplify compilation time and rebuilding dependencies.

## Use Object Based .h and .cpp

+ If you have more than 150 lines in your program then separate out any classes / structs into their own .h and .cpp. 
+ Note that .h files should only have inline methods.    
+ If the lab says do a seperate .h / .cpp then do it, even if your program is small.
+ For Template classes (136) you can ignore this since there is a known bug here.  

## Always Use Namespaces

There is almost never a reason to declare an identifier in the global namespaces. Instead, functions and classes should exist in an appropriately named namespaces or in a class inside of a namespace. Identifiers which are placed in the global namespace risk conflicting with identifiers from other (mostly C, which doesn't have namespaces) libraries.

136:  Do not bring in the whole std namespace in labs,  Instead site each individual element.  ie std::cout or std::endl 
126:  You can bring in namespace std and I'd encourage you to start getting in the habit of using std::cout.
116:  You can use "using namespace std"

## Avoid Compiler Macros

Compiler definitions and macros are replaced by the pre-processor before the compiler is ever run. This can make debugging very difficult because the debugger doesn't know where the source came from.

```cpp
// Good Idea
namespace my_project {
  class Constants {
  public:
    static const double PI = 3.14159;
  }
}

// Bad Idea
#define PI 3.14159;
```


### Strive to be const correct
Reference:  https://isocpp.org/wiki/faq/const-correctness
Bottom Line:  If you aren't updating it, tell the compiler.  For example:
<li> Any function that doesn't update the member data should be const.
<li> Parameters that aren't updated are call by value (native data types) or const parm & (classes)
