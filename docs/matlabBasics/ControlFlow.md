# Control Flow

*for Making Decisions or Repeating Stuff*

![][L-img-water-flow]

[L-img-water-flow]: images/traffic_jam.png

## Overview

*If, then, else, when?*

Control flow are the flow charts of computer programming. Control Flows allow you to create scripts or functions that execute or repeat upon meeting certain conditions. Think of a music player. When you click "Play", the Music plays. That is a type of control flow known as a "conditional statement." Similarly, when you select the "Repeat" function, the same song will play over and over. That is another type of control flow called a loop. We'll talk about that here too.

### Mildly Useful MATLAB Documentation

- [Loops and Conditional Statements](https://www.mathworks.com/help/matlab/control-flow.html')

- [if, elseif, else](https://www.mathworks.com/help/matlab/ref/if.html')

- [for loops](https://www.mathworks.com/help/matlab/ref/for.html')

- [while loops](https://www.mathworks.com/help/matlab/ref/while.html')

- [switch, case, otherwise](https://www.mathworks.com/help/matlab/ref/switch.html')

### Keywords you should know

- for
- while
- if
- else
- case
- otherwise
- [end](https://www.mathworks.com/help/matlab/ref/end.html')
- [return](https://www.mathworks.com/help/matlab/ref/return.html')
- [continue](https://www.mathworks.com/help/matlab/ref/continue.html')
- [break](https://www.mathworks.com/help/matlab/ref/break.html')

### Terminology you should know

- **Control Flow:** the process of creating conditional statements or looping statements.

- **Conditional Statement:** A statement used determine which block of code to execute at run time

- **Looping Statement:** A statement designed to repeatedly execute a block of code

---

## Conditional Statements

![][L-img-xkcd]

[L-img-xkcd]: images/xkcd_flow_charts.png "Flow Charts"

[xkcd](https://xkcd.com/518)

When programming, you often want the computer to respond differently depending on the input. Say for example that you have designed a facial recognition algorithm for your robot servant and you would like your robot servant to greet you and your family members by your proper names. Furthermore, you would like your robot servant to announce "Intruder Alert!", whenever encountering any person not recognized by the facial recognition algorithm, and to then initiate defensive measures.

**Conditional statements** are like programmatic flow charts that analyze values of specified variables to determine which block of code should be executed. This is useful for handling unknown situations. For example,  different blocks of code should execute depending on whether or not your robot recognizes you (or your spouse).

A conditional statement typically contains a series of expressions that can resolve to either TRUE or FALSE. Each expression is followed by the block of code to be executed if the expression resolves to TRUE. So, for conditional statements to properly work, only ONE expression should resolve to TRUE on a given run of the statement.  

Here is a pseudo-code version of a conditional statement:

```
IF MASTER RECOGNIZED
	greet MASTER as "Mr. Smith"
OR MISTRESS RECOGNIZED
	greet MISTRESS as "Mrs. Smith"
OTHERWISE
	attack INTRUDER
```

In this example, the expressions are shown in ALL CAPS, while the executable blocks are in lower case. Notice that, depending on the expression, only one of the executable blocks will execute.

### IF ELSE statements

IF, ELSE statements are the simplest and most straight forward of the conditional statements. They are used to create  programmatic flow charts.

!!! abstract "Anatomy of an IF ELSE STATEMENT"
    IF ELSE statements are bracketed by the `if` and `end` keywords. Optionally, they can contain **elseif** and **else** keywords. If you want to evaluate more than one *expression*, you need the **elseif** keyword.

    >**if** *expression*
    >
    >>CODE BLOCK 1
    >
    >**elseif** *expression*
    >
    >> CODE BLOCK 2
    >
    >**else**
    >
    >>CODE BLOCK 3
    >
    >**end**

    - *Expressions* can be logical operations, or simply numeric values, where `0` is `false`, and anything other than `0` is `true`
    - *Expressions* are evaluated in sequential order.
    - If the *expression* is `true`, the relevant block of code that immediately follows the *expression* is executed
    - If the *expression* is `false`, the next *expression* is evaluated.
    - If no *expressions* are `true`, and there is an **else** keyword, the block of code following the **else** keyword is executed (CODE BLOCK 3)
    - If there is no *else* keyword and none of the *expressions* are `true`, nothing happens.

Consider the following example:

```matlab linenums="1" title="Example: IF ELSE"
x = randi(10,1,1) % generate a random number

if rem(x,2) == 1
    display('x is odd')
else
    display('x is even')
end
```

In **line 1**, we set the value of `x` to a random integer (with a maximum possible value of 10) using the **`randi`** function. **Line 3** contains the **expression** (after the `if` keyword). This expressions evaluates whether or not the [remainder after dividing by 2](https://www.mathworks.com/help/matlab/ref/rem.html) IS EQUAL TO `1`. Recall that dividing an odd integer by 2 returns a remainder of 1.
 Depending on what random number x is set to, we will get the following:

1. If x is odd, **`rem`** will return a 1, the expression will return a`true`, and the first code block will be executed.
2. if x is even, then **`rem`** will return a 0, the expression will return a `false`, and second code block (line 6) will be executed.

### Adding multiple expressions (elseif)

If you need to evaluate multiple, sequential  *expressions*, you can use the `elseif` keyword in an IF ELSE statement.

In the following example, we will use an IF ELSE statement to characterize the inputted number.

```matlab linenums="1" title="IF ELSE with Multiple expressions"
x = 19
if isprime(x) % tests whether a number is prime
    str = 'a prime number';
elseif ~rem(sqrt(x),1) % tests for a perfect square 
    str = 'a perfect square'
elseif ~rem(log2(x),1) % tests for a power of 2
    str = 'a power of 2'
else
    str =  'none of the above';
end

fprintf('%d is %s\n', x, str) % fprintf outputs directly to the command window
```

Here is some terminology to recall as you review the code:

- **Prime Number**: a number divisible only by itself and 1
- **Perfect square**: a number that when you take the square root, you get a whole number
- **Power of 2**: a number in the form $2^n$

In this IF ELSE statement, we have several expressions to categorize the inputted number. The function [**isprime**](https://www.mathworks.com/help/matlab/ref/isprime.html) tests whether the number is prime. The function [**rem**](https://www.mathworks.com/help/matlab/ref/rem.html) returns the remainder after division (just like [**mod**](https://www.mathworks.com/help/matlab/ref/mod.html)). As shown here, this function can be very useful in characterize numbers in a variety of ways (1).
{ .annotate}

1. `~rem(sqrt(x),1)` - A perfect square should be a whole number after taking the square root. So, in this syntax, we take the square root of the inputted number, *x*, and then ask if there is any remainder after dividing by 1. For example, if the square root is not a whole number (like `1.4142`), then we would get a remainder (like `0.4142`). Whole numbers will return a zero after division by 1 (no remainder). So, to make this expression resolve to true when we do get a zero, we flip the script, using the LOGICAL NOT special character). We use a similar logic for powers of 2.

Note, IF ELSE expressions are **always evaluated sequentially**, starting with the first IF expression. So, the order of the *expressions* is a critical consideration. For example, 16 is both a perfect square and a power of 2. In this IF ELSE statement, 16 will be only be reported as a perfect square. It will never get a chance to be tested on whether it is also a power of 2. That expression will just be skipped.

#### ADVANCED CHALLENGE: elseif

=== "Question"
    Review the IF ELSE Statement above and add the following functionality:

    1. Reports if the Number is 'odd, but not prime' using the following expression `rem(x,2)`, which returns a 1 for odd numbers
    2. Reports if the number is even

=== "Answer"

    ```matlab
    if isprime(x) % tests whether a number is prime
        str = 'a prime number';
    elseif ~rem(sqrt(x),1) % tests for perfect squares
        str = 'a perfect square';
    elseif rem(x,2) % tests for odd numbers 
        str = 'odd but not prime';
    elseif ~rem(log2(x),1) % tests for powers of2
        str = 'a power of 2!';
    else % assumes number is even
        str =  'even';
    end
    fprintf('%d is %s\n', x, str) % fprintf outputs directly to the command window
    ```

    1. Note the position of the 'odd, but not prime' is right after the test for prime numbers
    2. Note that we don't have to test whether the number is even. We just assume once all of the other expressions resolve to false, that the number is even, so we place that report after the **`else`** keyword

---

## SWITCH CASE

You use SWITCH CASE when you just want to match the variable contents to a specific value, like 'red'. *Switch, case* statements are best used when you have an exact value you want to matched, such as a word or a number.

!!! abstract "Anatomy of a SWITCH CASE statement"

    SWITCH CASE statements use the `switch` and `case` key words. These Conditional Statements execute depending on the value of the indicated  *variable*. If the value in *variable* matches the value in one of the CASE lines, then corresponding block of code is executed. If there are multiple matches, only the first match is executed. If there is no match, the code block following the **otherwise** keyword is executed. The **otherwise** keyword is optional, and if not included, and there is not match, the SWITCH CASE statement simply exits and runs no code blocks.

    >**switch** *variable*
    >>**case** *value 1*
    >>>CODE BLOCK 1
    >>
    >>**case** *value 2*
    >>>CODE BLOCK 2
    >>
    >>**case** *value 3*
    >>>CODE BLOCK 3
    >>
    >>**otherwise**
    >>>CODE BLOCK 4
    >
    >**end**

    - The *variable* is indicated immediately after the `switch` keyword. This tells the statement to inspect the contents of variable. 
    
    - The potential *values* are listed after each `case` keyword.
    - If the *value* matches the content of the *variable*, the block of code immediately following the *value*  is executed.
    - Only one CODE BLOCK is executed per run.   

Consider the following example

```matlab linenums="1" title="Example: Switch, Case"
channel = 'red' % set channel value

switch channel
    case 'red'
        display('Roses are red')
    case 'green'
        display('Stems are green')
    case 'blue'
        display('Violets are blue')
    case 7
        display('Seven is a number')
    otherwise
        display('try again')
end
```

…Here, since the variable  *`channel`* contains the character array 'red',  only the code on line 5 will run: `display('Roses are red')`. If you change *`channel`* to 'green', 'blue', or 7, then that corresponding line of code will run (lines 7 and 11, respectively). If you change *`channel`* to *anything* else, like 'moon' or 4, then the *otherwise* code block `display('try again')` will run (line 13). Note: this SWITCH CASE statement is case-sensitive. So, you if you change *`channel`* to 'Red', then the *otherwise* code block will execute.

## Loops

**Looping Statements** are used to repeatedly execute the same code block over and over while modifying the values of certain variables. Computers are really good at repeating tasks over and over, sometimes to a fault. For example, depending on the size of the intruder, you may want your robot to repeatedly deliver non-lethal roundhouse kicks to intruder's face until he or she is incapacitated. A FOR LOOP can help you with that, but if you don't program the loop properly, you run the risk of over-delivering roundhouse kicks to the intruder's face.

### FOR LOOPS

FOR LOOPS are used to repeatedly execute a CODE BLOCK for a predetermined number of times.

!!! abstract "Anatomy of a FOR LOOP"

    A FOR LOOP statement is bracketed by the `for` and `end` keywords. In between is the block of code that is run repeatedly.
    
    > **for** *index = values*
    >
    >>CODE BLOCK
    >
    > **end**

    1. Notice immediately following the the `for` keyword is an initializing statement that resembles a variable assignment
    2. This *initializing statement* determines how many times the LOOP will run
    3. The number of times that the loop will run equals the number of columns in *values*.
    4. On each iteration of the loop, the *index* will pull a value from a subsequent column in *values*. So, *index* will have a different value on each iteration. 
  
For example, consider the following:

```matlab linenums="1" title="FOR LOOP"
for i = 1:10
	fprintf('The value of i is %d\n',i)
end
```

These 3 lines set up the entire *for loop* statement.

- **Line 1** contains the the *initializing statement* (right after the `for` keyword). This *initializing statement* creates a horizontal vector `i` containing the integers 1 through 10. Since there are 10 *horizontal* elements, the FOR LOOP will run 10 times.
- **Line 2** contains the executed line of code:
  > `fprintf('The value of i is %d',n)`
- In **Line 2**, the variable *`i`* refers to current element in the vector set-up in in the *initializing statement*. So, on the first loop, *`i`* equals 1. On the second loop, *`i`* equals 2, etc.

After the above FOR LOOP is complete, you should see the following output in the command window:

```matlab title="Output after FOR LOOP"
The value of i is 1
The value of i is 2
The value of i is 3
The value of i is 4
The value of i is 5
The value of i is 6
The value of i is 7
The value of i is 8
The value of i is 9
The value of i is 10
```

...This output is the result of executing the **`fprintf`** function over and over again while only changing the value of *`i`* on each iteration.

!!! note "Important Notes About For Loops"

      - **FOR LOOPS** will loop the number of times equal to the number of columns in the array of the *initializing statement* (not the maximum value in the array)

      - You can use any variable name in the *initializing statement* (*n* and *i* are popular variable names for **FOR LOOPS**), or you could even use a vector array that has already been created

      - The **FOR LOOP** initializing array does not have to start with the value 1

---

### Challenge - For Loop

=== "QUESTION"

    How many times will the following **FOR LOOP** loop?

    ```matlab linenums="1"
    for m = 2:2:10
        fprintf('The value of m is %d\n',m)
    end
    ```

    - Also, what will be displayed in the command window after execution of the FOR LOOP is complete?

=== "Answer"

    - This **FOR LOOP** loop will loop **5 times**
    - The following will be displayed:
    
    ```matlab title="result"
    The value of m is 2
    The value of m is 4
    The value of m is 6
    The value of m is 8
    The value of m is 10
    ```

---

### Preallocation

FOR LOOPS are often used to fill arrays in some sequential fashion, such as element-by-element or row-by-row. When doing this, you should always *[preallocate](http://www.mathworks.com/help/matlab/math/resizing-and-reshaping-matrices.html#f1-88760)* the array, meaning that you should create an empty array that already contains the number of elements that you want to end up with. Then, during the execution of the loop, you simply fill each element of the array with the data that you want. If you know how big your final array is going to be, preallocation is easily accomplished using the function **[zeros](http://www.mathworks.com/help/matlab/ref/zeros.html),** which creates an array filled with zeros.  If you don't preallocate, MATLAB has to create a copy of the variable on each iteration of the loop which takes more time and uses more memory. 

For  example, the following creates an array *i* with 10 zeros

```matlab linenums="1"
i = zeros(1,10)
```

```matlab title="result"
i =
    0     0     0     0     0     0     0     0     0     0
```

You can fill the elements of *i* using a **FOR LOOP** as follows:

```matlab linenums="1"
for n = 1:10
 i(n) = n*10
end
```

On each iteration of the loop, you fill one element and get an output that looks like the following

```matlab title="Filling an array using a FOR LOOP"
i =
    10     0     0     0     0     0     0     0     0     0 % iteration 1
i =
    10    20     0     0     0     0     0     0     0     0 % iteration 2
i =
    10    20    30     0     0     0     0     0     0     0 % iteration 3
i =
    10    20    30    40     0     0     0     0     0     0 % iteration 4
i =
    10    20    30    40    50     0     0     0     0     0 % iteration 5
i =
    10    20    30    40    50    60     0     0     0     0 % iteration 6
i =
    10    20    30    40    50    60    70     0     0     0 % iteration 7
i =
    10    20    30    40    50    60    70    80     0     0 % iteration 8
i =
    10    20    30    40    50    60    70    80    90     0 % iteration 9
i =
    10    20    30    40    50    60    70    80    90   100 % iteration 10
```

…As you can see in the Command Window output, each run of the FOR LOOP adds a multiple of *`n`* into the nth element of *`i`*. Notice how the zeros are being replaced with the data.

### Vectorization

The term **vectorization** refers to the creation an array simply by using the MATLAB syntax of array creation (without the use of a FOR LOOP). Indeed, it is often possible to create an array without needing a FOR LOOP in MATLAB. This is known as vectorizing a FOR LOOP. You should always try to vectorize your code whenever possible as the vectorized form of the code can run faster than the FOR LOOP form.

For example,

```matlab
j = [1:10] * 10

j =
    10    20    30    40    50    60    70    80    90   100
```

…accomplishes the same thing as the previous loop, but uses only one line of code and no looping.

### Combining Conditional Statements and FOR LOOPS

Control Flow statements are often used in combination. Consider the following:

```matlab linenums="1" title="a FOR LOOP containing an IF ELSE statement"
for x = 1:10
    if rem(x,2) % test for odd numbers
        eo = 'odd';
    else % if not odd, its even
        eo = 'even';
    end
    
    fprintf('\nThe number %d is %s\n',x,eo)
end
```

…This FOR LOOP runs 10 times. On each iteration, the IF, ELSE conditional statement checks whether the current value of `x` is odd or even and sets the value of `eo` accordingly. The function **`fprint`** prints the result to the command window as follows

```matlab title="result"
The number 1 is odd
The number 2 is even
The number 3 is odd
The number 4 is even
The number 5 is odd
The number 6 is even
The number 7 is odd
The number 8 is even
The number 9 is odd
The number 10 is even
```

---

## WHILE LOOPS

WHILE LOOPS are used to repeatedly execute a block of code until a condition is met.

!!! annotation "Anatomy of a WHILE LOOP"
    
    WHILE LOOPS are bracketed by the **while** and **end** keywords. The **while** keyword is followed by an *expression* that resolves to `true` or `false`

    >**while** *expression*
    >
    >>CODE BLOCK
    > 
    >**end**

WHILE LOOPs loop indefinitely until the *expression* resolves to `false`. On each iteration of the WHILE LOOP, the *expression* is evaluated. If the expression evaluates to `true`, then the looping continues.  So, the variable being evaluated in the expression must change in the block of code for the looping to ever stop. This also means that if you are not careful with your code and the *expression* never resolves to `false`, the WHILE LOOP will NEVER STOP LOOPING!

!!! tip "Breaking out of Stuck WHILE LOOPS"
    Sometimes while loops can be trapped in an unbreakable loop (usually due to shoddy programming). To forcefully a break out of a **while loop**, enter  `Ctrl-C`.

Consider the following:

```matlab linenums="1" title="Example: WHILE LOOP"
n = 1
while n<10
    disp(n)
    n = n+1;
end
```

This loop simply displays the value of *n* each time the loop iterates. And then increments the value of *`n`* by 1. Notice that the code inside the loop does not execute once the value of *n* reaches 10. Once *n*=10, the expression `n<10` resolves to FALSE and the loop stops executing (and doesn't execute the code after the WHILE line).

### Challenge - While LOOP 1

=== "Question"

    How would you change the above example to make the WHILE LOOP stop iterating after the value of *`n`* reaches 20?

=== "Answer"

    You change the expression to `n<20`

    ```matlab linenums="1"
    n = 1
    while n<20
        disp(n)
        n = n+1;
    end
    ```

---

So, why bother with WHILE loops? The code above could easily be accomplished using a FOR LOOP. The main reason that you use a WHILE is for situations when you don't know beforehand when the repeating code should stop executing.

Consider the following code which the simulates the sequential rolling of a die until a 5 is rolled

```matlab linenums="1" title="Example: WHILE LOOP"
die = 1; % initial value of die is set to 1
while die ~=7
    fprintf('You rolled a %d. Try again.\n',die) % report the die value
    die = randi(6,1,1); % randomnly assign a new value to the die (1-6)
end
fprintf('You rolled a %d. Nice Job!',die);
```

When you are rolling an actual die, there is no way to guess when you are going to roll a 5. You just have to roll until you get a 5. 

In this example, we use the function [**randi**](https://www.mathworks.com/help/matlab/ref/randi.html) to randomly return an integer between 1 and 6. Each time the WHILE LOOP iterates, **randi** returns a different integer. The WHILE LOOP will continue to iterate until *die* is randomly set to the value `5`.

Here is the output I got the last time that I ran the code:

```matlab title="WHILE LOOP output"
You rolled a 1. Try again.
You rolled a 1. Try again.
You rolled a 2. Try again.
You rolled a 1. Try again.
You rolled a 1. Try again.
You rolled a 5. Nice Job!
```

Notice that I needed two calls for **`fprint`**: one for inside the LOOP to report the current value of *die*, prior to changing its value, and one outside of the LOOP to report the final value of the die.

If you run this code in MATLAB, you will very likely get a different output. Try it now!

### Challenge - While LOOP 2

=== "Question"
    What would you change in the code above so that the WHILE LOOP stops iterating after "rolling" a 3 instead of a 5?

=== "Answer"
    You would Change the conditional expression to:

    `while die ~=3`

    as follows

    ```matlab linenums="1"
    die = 1; % assign die value of 1
    while die ~=3 % <== Change the 5 to a 3 here
        fprintf('You rolled a %d. Try again.\n',die) % report the die value
        die = randi(6,1,1); % randomly assign a new value to the die (1-6)
    end
    fprintf('You rolled a %d. Nice Job!',die);
    ```

---

### A More Advanced WHILE LOOP Example

Warning. This example involves math.

To further explore WHILE LOOPS, let's consider the following the illuminating example:

>You receive an allowance of `$20` per week, `$6` of which you immediately spend on candy and soda. This is a non-negotiable expense. Recently, all your friends got hoverboards, and you want one too. But hoverboards currently cost `$100`, and you only have `$20` in your bank account. Worse, due to the surge in popularity, hoverboard prices have been steadily increasing in price by roughly `3%` each week. You want to know how many weeks it will take to save up for a hoverboard, assuming your allowance and candy and soda expenses remain constant.

Manually, you could solve this problem by calculating your weekly net income ($14), adding that amount to your bank account, and then comparing the amount in your bank account to the current price of the hoverboard. Remember, the hoverboard price increases each week, so you will have to recalculate the current price of the hoverboard. If your bank account is less than the amount of the hoverboard, then you recalculate the bank  balance and hoverboard price until you have more money in your bank account than the updated price of the hoverboard. To determine how long this will take, you count the number of times you had to repeat the recalculation process (saved), which is equivalent to the number of weeks until you're cruising on your sweet, sweet hoverboard.

A WHILE LOOP can automate the recalculation process as follows:

```matlab linenums="1"
week = 0; % starting at week zero
bank_account = 20; % current bank balance 
candy_soda_expense = 6; % non-negotiable weekly expenses
allowance = 20; % weekly income
hoverboard = 100; % starting price of the hoverboard

while bank_account < hoverboard % iterate while bank account is less than hoverboard price
    bank_account = bank_account - candy_soda_expense + allowance; % recalculate weekly bank balance
    hoverboard = hoverboard + hoverboard * 0.03; % price increases by 3% each week
    week = week + 1; % iterates the week count
end

fprintf('The number of weeks to save up for a hoverboard is %d.\nThe price of the hoverboard will be %1.2f.\nYou will have %1.2f in your bank account\n', week, hoverboard, bank_account)

```

…Prior to the start of the loop, we preallocate several variables that will be used inside the loop.

- *`bank_account`*: keeps track of your current bank balance, starts at $20
- *`hoverboard`*: keeps track of the increasing price of hoverboards, starts at $100
- *`candy_soda_expense`*: your weekly expense, $6 on candy and soda
- *`allowance`*: your weekly income, $20/week
- *`week`*: a variable used to track the number of weeks.

At the start of the loop, the WHILE relative *expresssion* `bank_account < hoverboard` is evaluated. If bank_account is below hoverboard, the relative operation returns a `TRUE`, and the LOOP starts. Inside of the loop are the steps need to recalculate the balance in your bank account and the price of hoverboard. On each iteration of the loop, the value of *`bank_account`* and *`hoverboard`* are recalculated and *`week`* increases by 1. If, `bank_account < hoverboard`, then the WHILE loop continues to iterate. When `bank_account < hoverboard` is NOT TRUE, the WHILE LOOP code block is skipped and then the line after the WHILE LOOP executes (the line with the function **`fprint`**), which prints the results to the command window.  

And as we can see below, the result is:

```matlab title="Final Result"
The number of weeks to save up for a hoverboard is 8.
At this time, the price of the hoverboard will be 126.68
and you will have 132.00 in your bank account.
```

### Challenge - WHILE LOOPS 3

=== "QUESTION"

    How many weeks would it take if:

    -  you eliminate your Candy and Soda expense? (and everything else was at the original setting)?
    -  You allowance was only $15?
    -  The starting price of a Hoverboard was $150?
    -  You already had $100 in your bank account?

    …When answering the above questions, assume that all other variables are reverted back to their original defaults

=== "Answer"
    How many weeks would it take if: (Remember, answer each question assuming all other variables are reverted back to their original defaults).

    To answer these questions, you simply change the starting values of the variables prior to the start of the WHILE LOOP. Don't change anything inside the loop. Be sure to change all the variables back to the default values, before adjusting the value of any 1 variable. 

    -  ...your Candy and Soda expense was $0 (and everything else was at the original setting)?
    > 5 weeks
    -  ...your allowance was $15?
    > 16 weeks
    -  ...hoverboards cost $150?
    > 16 weeks
    -  ...your starting bank_account amount was $100
    > 0 weeks. The WHILE LOOP doesn't even start because 100 is NOT less than 100.