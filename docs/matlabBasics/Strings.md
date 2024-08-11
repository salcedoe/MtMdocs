# String Arrays

!!! abstract "*for better wrangling of characters, especially words*"

🧶 String arrays are designed to manage collections of character arrays. They have only recently been added to MATLAB, but they have quickly become a powerful tool for managing collections of characters and words. 

## Overview

This module is broken down into the following sections:

---

### Things you should know

After completing this module, you should be able to:

* Differentiate between a Character and a String Array.
* Assign values to string arrays using paired double quotes `" "` and square brackets  `[ ]` 
* Index string arrays using both `( )` and `{ }` be able to predict the outcome of each
* Manipulate string arrays using mathematical operators such as `+` and logical operators such as `==` 
* Use the functions found on the [Character and String Reference Page][char-string-page] 

### Relevant Mathworks Documentation

- The  <a href="MATLAB:web(fullfile(docroot, 'matlab/ref/string.html'))">string</a> documentation page
- The <a href="MATLAB:web(fullfile(docroot, 'matlab/characters-and-strings.html?s_tid=CRUX_lftnav'))">Characters and String Reference Page</a>
 
### Special MATLAB Characters

*  `" "` - paired double quotes: for creating string arrays
*  `[ ]` - square brackets: for concatenation
*  `( )` - parentheses: for indexing
*  `{ }` - curly brackets:  for extract contents from string array elements

---
## But First, a Bit of Background

Why do we need another variable type just to manage a bunch of letters?

### The Trouble With Character Arrays

Recall our issue with multi-row character arrays:

```matlab linenums="1" title="Padding Character Arrays"
chary = char('one fish', 'two fish', 'red fish', 'blue fish')
```

```matlab title="result"
chary =

  4×10 char array

    'one fish  '
    'two fish  '
    'red fish'
    'blue fish '
```

To create character array matrices, we needed the function **`char`** to properly pad the rows of the matrix with enough spaces so that there are an equal number of characters in each row (recall that `space` is a character). But this becomes burdensome rather quickly. For every new row added to a character array, the entire array needs to be re-padded with spaces. Worse, those extraneous spaces in a large character array take up valuable memory for no reason. There had to be a better way.

### The Cell Array Kludge

For the longest time, the cell array was the better way to package character arrays. In fact, this remains one of the best uses for cell arrays. In a cell array, each row of a character array can simply be added to one of the cell elements, no space-padding required. For example:

```matlab linenums="1" title="Concatenating words in a cell array"
celly = {'one fish'; 'two fish'; 'red fish'; 'blue fish'}
```

```matlab title="result"
celly =

  4×1 cell array

    {'one fish' }
    {'two fish' }
    {'red fish' }
    {'blue fish'}
```
 
And this worked for many years, but it was a kludge. Cell arrays were designed to package disparate variable types into a single variable. It is easy to package things into cell arrays, but harder to get them out. And the indexing is unnecessarily complex. Worse, due to its promiscuous proclivities (you can store *anything* in a cell array), the cell class has large memory overhead and few functions designed specifically for managing character arrays.  

## String Array Rising

Enter **string arrays** - the leaner and meaner variable class designed from the ground up to wrangle character arrays.

The syntax is fairly simple. Instead of single quotes, you use double quotes. And you concatenate using square brackets, like numeric arrays. For example, the following syntax creates a string array called *`stringy`*

```matlab linenums="1" title="Concatenating words in a string array"
stringy = ["one fish", "two fish", "red fish", "blue fish"]'
```

```matlab title="result"
stringy = 

  4×1 string array

    "one fish"
    "two fish"
    "red fish"
    "blue fish"

```

…Notice here that we used the transpose operator `'` to orient our new string array, *`stringy`*, as a column vector. Also notice that *`stringy`* requires less bytes to store in memory than *`celly`*: 336 vs 518 bytes, a more than 60% reduction in memory requirement.

---
### Indexing String arrays


String arrays follow the same indexing syntax rules of other complex variable types. Indexing with parentheses `()` returns a smaller string array, whereas indexing with the curly brackets `{}` returns the contents of the elements (or in this case, the character array contained within).

For example, to return the first element from *`stringy`* as a scalar string array, we use the parentheses as follows:

```matlab linenums="1" title="Indexing element 1 in a string array"
 stringy(1)
```

```matlab title="result"
ans = 

    "one fish" % the first element in the string array
```

…We can tell that *`ans`* is a string array because the characters in the result are bracketed by double quotes: `"one fish"` (or, by examining the properties of *`ans`* in the workspace).

To unpack the first element from stringy and access the character array, we use the curly brackets `{}` as follows:

```matlab linenums="1" title="Unpacking String Array element 1"
stringy{1}
```

```matlab title="result"
ans =

    'one fish' % the character array contents from the first element
```

…Here, we can tell that *`ans`* is a character array because the outputted result is bracketed by single quotes:  `'one fish'` (or, by examining the properties of *`ans`* in the workspace)

We can use keywords, such as `end`, to return a string element, as follows:

```matlab linenums="1"  title="Index Last element"
stringy(end)
```

```matlab title="result"
ans = 

    "blue fish"
```

 …this syntax returns the last element in *`stringy`* as a smaller string array

Or we can use complex indexing that uses both parentheses and curly brackets. For example, the following syntax returns the last character in the first element of *`stringy`*:

```matlab linenums="1" title="Unpacking the last character from element 1"
stringy{1}(end)
```

```matlab title="result"
ans =

    'h' % the last character in element 1 of the string array
```

…In this syntax, the curly bracket extracts the contents from the first element in *`stringy`*, while the parentheses are used to index out the last character from that extracted character array, which happens to be the letter `h` from the word fish.

### Concatenating string arrays

String arrays also have syntax reminiscent of manipulating numeric arrays. For example, we can easily add more rows to our friend *`stringy`*, using following syntax:

```matlab linenums="1" title="Concatenating String Arrays"
stringy = [stringy; "black fish"; "blue fish"; "old fish"; "new fish"]
```

```matlab  title="result"
stringy = 

  8×1 string array

    "one fish"
    "two fish"
    "red fish"
    "blue fish"
    "black fish"
    "blue fish"
    "old fish"
    "new fish"
```

…Notice the use of recursive assignment, where the variable name `stringy` appears on both sides of the assignment operator `=`. This means overwrite `stringy` with a new version of itself that contains all of its original elements, plus a bunch of fun new string elements (four new elements, to be precise). Also notice the use of semi-colons to indicate the addition of elements vertically.

### String array 'arithmetic'

We can use the `+` operator to quickly append characters to each element of a string. For example, the following syntax appends a comma to the end of each element in *`stringy`*:

```matlab linenums="1" title="Appending a comma to each element in the string array"
stringy = stringy + ',' 
```

```matlab title="result"
stringy = 

  8×1 string array

    "one fish,"
    "two fish,"
    "red fish,"
    "blue fish,"
    "black fish,"
    "blue fish,"
    "old fish,"
    "new fish,"
```

…Notice that we didn't even need to have the same sized arrays for the operation. MATLAB simply assumed we wanted to append the `,` to the end of each character arrays in *`stringy`*. This syntax is reminiscent of when we add a scalar to a vector: MATLAB assumes that you want to add the scalar to each element of the vector.

### Challenge: String Array Indexing

=== "Question"
    How would you use complex indexing (using both the parentheses and the curly brackets) to replace the last comma in the last element of *`stringy`* ("new fish,") with an exclamation point?
=== "Answer"

    We can replace that last comma in the last element with an exclamation point with the following syntax:

    ```matlab linenums="1" title="Replace comma with exclamation point"
    stringy{end}(end) = '!'
    ```

      - Here, we first unpack the contents from the last element in *`stringy`* using the curly bracket syntax: `{end}`. 
      - Then, we index the last element (a `,`) from unpacked character array `'new fish,'` using the parentheses syntax: `(end)`
      - Then, we use the assignment syntax (`=`), to replace the comma `,` with an exclamation point (`!`).
      - Et voila:

    ```matlab title="result"
    stringy = 

      8×1 string array

        "one fish,"
        "two fish,"
        "red fish,"
        "blue fish,"
        "black fish,"
        "blue fish,"
        "old fish,"
        "new fish!"
    ```

### Relational operations on string arrays

You can also use relational operations on a string array in an intuitive manner.

!!! example "Relational Operation IS EQUAL TO"
     For example, if you want to find the element in  *`stringy`* that matches the character array 'two fish,' you would use the following syntax:

    ```matlab linenums="1" title="Find Elements that match 'two fish,'"
    stringy == "two fish," 
    ```

    ```matlab title="Result"
    ans =

      8×1 logical array

      0
      1
      0
      0
      0
      0
      0
      0
    ```

    …only the second element contains "two fish,".

!!! example "Relational Operation IS NOT EQUAL TO"

    Or if, say, you wanted to find all elements that do not contain "blue fish," you would use this syntax:

    ```matlab linenums="1" title="Find elements that do not match 'blue fish,'"
    stringy ~= 'blue fish,'
    ```

    ``` matlab title="result"
    ans =

      8×1 logical array

      1
      1
      1
      0
      1
      0
      1
      1
    ```

    …here, only elements 4 and 6 match 'blue fish,'.  Elements 1,2,3,5,7, and 8 do NOT match.

Notice that in the above examples, we are matching the entire contents of each element in *`stringy`* to the character array. If they don't match precisely, we won't get a match.

```matlab linenums="1" title="Elements that Contain 'blue fish'"
stringy == 'blue fish'
```

```matlab title="Result returns no match"
ans =

  8×1 logical array

   0
   0
   0
   0
   0
   0
   0
   0
```

... The syntax above finds no matches because we didn't include the `,` in the character array at the end of the character array 'blue fish'.

---

## String Array Functions

MATLAB has many functions to manipulate and process string arrays. You can find a list of them on the  <a href="MATLAB:web(fullfile(docroot, 'matlab/characters-and-strings.html?s_tid=CRUX_lftnav'))">Characters and String Reference Page</a>. These functions are grouped into the following categories:

- Create, Concatenate, Convert
- Determine Type and Properties
- Find and Replace
- Join and Split
- Edit
- Compare
- Regular Expressions

Familiarize yourself with these functions to find many powerful ways to manipulate string arrays. The following are just a few examples.

### Example: Contains

!!! example "contains"

    Say we want to find the elements in *`stringy`* that contain the character array 'blue', we can use the function **`contains`** as follows:

    ```matlab linenums="1" title="Elements that contain 'blue'"
    contains(stringy,'blue')
    ```

    ```matlab title="result"
    ans =

      8×1 logical array

      0
      0
      0
      1
      0
      1
      0
      0
    ```

    …And we get a couple of matches (elements 4 and 6). Notice here that we don't have to match the entire content of an element in *`stringy`*, just a portion of the contents. Whereas, in the previous section, we needed a precise match when we used the logical operation `==`. 

    We can even match just a single character as follows:

    ```matlab linenums="1" title="Elements that contain the character 'w'"
    contains(stringy,'w')
    ```

    ```matlab title="result"
    ans =

      8×1 logical array

      0
      1
      0
      0
      0
      0
      0
      1
    ```
    …This syntax returns all elements that contain the letter `w` in them (`two` and `new`, in this case).

### Example: Replace

!!! example "replace"

    The function **`replace`** is a quick way to replace one character array with another. Consider our friend *`stringy`*. We can easily replace `"fish"` with `"squish"` using the following syntax:

    ```matlab
    squishy = replace(stringy, 'fish', 'squish')

    squishy = 

      8×1 string array

        "one squish,"
        "two squish,"
        "red squish,"
        "blue squish,"
        "black squish,"
        "blue squish,"
        "old squish,"
        "new squish!"
    ```

### Example: Split

!!! example "split"

    The function *`split`* splits character arrays at the indicated delimiter (such as space, the default delimiter):

    ```matlab linenums="1" title="Split string array at space"
    splity = split(squishy)
    ```

    ```matlab title="Result is a new 8x2 string array"
    splity = 

      8×2 string array

        "one"      "squish,"
        "two"      "squish,"
        "red"      "squish,"
        "blue"     "squish,"
        "black"    "squish,"
        "blue"     "squish,"
        "old"      "squish,"
        "new"      "squish!"
    ```

    …The variable *`splity`* has two columns. The first column contains all of the characters preceding the `space` delimiter while the second column contains all of the characters that follow the delimiter.

### Example: Erase

!!! example "erase"

    If we decide we don't want any punctuation in our string array after all, we can use the **`erase`** function to quickly remove the offending punctuation, as follows:

    ```matlab
    erase(splity, ["," "!"])

    ans = 

      8×2 string array

        "one"      "squish"
        "two"      "squish"
        "red"      "squish"
        "blue"     "squish"
        "black"    "squish"
        "blue"     "squish"
        "old"      "squish"
        "new"      "squish"
    ```

    As you can imagine, the examples are endless. Refer to the [reference page][char-string-page] as needed or for inspiration.

Module Complete 🧶

---
[char-string-page]: https://www.mathworks.com/help/matlab/characters-and-strings.html