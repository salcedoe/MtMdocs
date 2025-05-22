# Functions

!!! abstract "*For doing stuff*"

## Stuff You Should Know

* That a function does stuff with variables
* That there are a lot of functions
* How to find built-in MATLAB functions
* How to call functions using the proper syntax.

## Useful-ish MATLAB Documentation

* [Calling Functions](http://www.mathworks.com/help/matlab/learn_matlab/calling-functions.html){target="_blank"}

## So, What is a Function?

A function takes the data from a variable and does stuff. Think of a function as a list of instructions typically designed to manipulate the inputted data in some fashion. If you want to get fancy, you can call it a [sub-routine](https://en.wikipedia.org/wiki/Subroutine){target="_blank"} or an algorithm. Often, these programming instructions are hidden from the user, so you can think of a function a little like a black box.

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

Of course, now that we are living in the future, MATLAB comes with an AI called  [MATLAB Copilot](https://www.mathworks.com/products/matlab-copilot.html){target="_blank"}. This is included with the Site License and should automatically be added to your MATLAB installation. Use this AI to help create code and troubleshoot errors. Your student CU Anschutz credentials also give you access to the latest version of ChatGPT through  [Microsoft Copilot](https://copilot.microsoft.com).
