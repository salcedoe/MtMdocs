# Functions

!!! abstract "*For doing stuff*"

## Stuff You Should Know

* That a function does stuff with variables
* That there are a lot of functions
* How to find built-in MATLAB functions
* How to call functions using the proper syntax.

## Useful-ish MATLAB Documentation

* [Calling Functions](http://www.mathworks.com/help/matlab/learn_matlab/calling-functions.html)

## So, What is a Function?

A function takes the data from a variable and does stuff. Think of a function as a list of instructions typically designed to manipulate the inputted data in some fashion. If you want to get fancy, you can call it a [sub-routine](https://en.wikipedia.org/wiki/Subroutine) or an algorithm. Often, these programming instructions are hidden from the user, so you can think of a function a little like a black box.

![Function as a Black Box][img_black_box]

[img_black_box]:images/black_box.png

The MATLAB syntax used to call a function looks like this:

```matlab
output = name_of_function(input_variable)
```

Notice that you will typically find the function on the right side of the equal sign. This is because a function typically (but not always) returns data that you can then stash into a variable.

## Getting Help on Functions

MATLAB has thousands of built-in functions to perform almost any basic task you can think of. So, sometimes the hardest part is:

1. Finding the right function to do exactly what you are looking for
2. Writing the proper syntax to call that function.

The MATLAB built-in documentation is a great place to start. You can find the available MATLAB functions and the proper syntax for calling those functions using the built-in documentation.

If you can't find it in the MATLAB documentation, then you can search the internet for MATLAB functions. There are a lot out there on MATLAB. When in doubt, *Google*. I typically preface my Google searches as follows:

```matlab
google matlab "thing I want to do"
```

>…but not necessarily with those double quotes.

Of course, now that we are living in the future, you can also use ChatGPT. Your student CU Anschutz credentials give you access to the latest version of ChatGPT through  [Microsoft Copilot](https://copilot.microsoft.com). Be sure to sign in to use the full version. The Mathworks even provides a [MATLAB ChatGPT Playground](https://www.mathworks.com/matlabcentral/playground/new) specifically for MATLAB. This might be the best place to start for using ChatGPT to answer your MATLAB-related questions.
