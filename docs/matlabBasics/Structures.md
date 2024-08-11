# Structures

!!! abstract *For Storing Related but Disparate Information in a Tree-like Format*

    "You're so beautiful, Like a tree" - Flight of the Conchords, [The Most Beautiful Girl in the Room
    ](https://www.youtube.com/watch?v=89zOtd6VAiU)

## Overview

🌳 Structure arrays have a hierarchal, trunk-and-branch data structure. They are useful for organizing disparate information and variable types into a single variable.

![image of a tree][img_tree]

[img_tree]: images/Gumbo_Limbo_Tree_DeSoto_National_Monument.jpg

### Learning Objectives

After finishing this module, you should be able to:

- Explain why you would use a structure array
- Compare a structure array to a cell and a character array
- Assign a value to a structure array using dot notation
- Access field content in a structure

### Relevant MATLAB Documentation

- [Structures][struct-ref-page]
- [Structure Functions][struct-fun-ref-page]

[struct-fun-ref-page]: https://www.mathworks.com/help/matlab/structures.html
[struct-ref-page]: https://www.mathworks.com/help/matlab/matlab_prog/create-a-structure-array.html

### Important Terminology

- **Structure**: a data type that groups related data using data containers called fields. Each field can contain data of any type or size.

- **Dot Notation**: using the period after a variable name to create or access structure fields

---

## Creating a Structure

A structure array is a hierarchal data structure that groups data into *fields*. Structure arrays are very useful for organizing complex data, such as the metadata from image files.


![img-name](images/struct_illustration1.png){ width="100"}

The good news about structures is that is very simple and intuitive to make a structure. Simply type a new variable name, append a period (`.`) to the end of the name, and then add a field name. This is known as *dot* notation.

For example, the following syntax creates a new structure called *`img_info`*, with three new fields: "filename", "rows", and "cols".

```matlab linenums="1" title="Creating a structure"
img_info.filename = 'moonshot.jpg'
img_info.rows = 25
img_info.cols = 50
```

```matlab title="Result: a new structure called img_info"
img_info = 

  struct with fields:

    filename: 'moonshot.jpg'
        rows: 25
        cols: 50
```

…Notice that fields can be of any data array class, including character and numeric.

## Accessing Field Content

To access the content from a field in a structure, you use *dot* notation, as follows:

```matlab linenums="1" title="Accessing fields in structures using dot notation"
img_info.rows
```

```matlab title="Result: the accessed data from img_info"
ans =

    25
```

!!! tip
    To automatically bring up a list of all of the filenames in a structure, do the following
    1. Type the variable name of the structure
    2. Type the dot (`img_info.`)
    3. Then hit the TAB button.
     
    A yellow dialog box containing all field names of the structure should appear. Once the field name dialog appears, select a field name using the UP and DOWN arrows and then ENTER. This technique is VERY useful when there are a lot of field names

    ![][img_struct_tab]

    [img_struct_tab]: images/struct_tab.png

## Creating an Array of Structures

Like all MATLAB variables, a structure can also be an array. This is a known as a Nonscalar Structure Array (remember, scalar means having just one element).

Think of it like this: each element in the array contains a structure. For this to work, all the  structures in the array must have the same fieldnames, but the data *stored* in the fieldnames can be different.

You  add new elements to a structure array as you would to a numeric array: by using the parentheses to indicate the index of the element.

!!! example "Nonscalar Structure Array"

    ```matlab linenums="1" title="Adding a new element to our Nonscalar Structure array"
    img_info(2).filename = 'apollo13.jpg'
    img_info(2).rows = 100
    img_info(2).cols = 200
    ```

    ```matlab title="Result: a 1x2 Nonscalar Structure Array"
    img_info = 

    1x2 struct array with fields…

        filename
        rows
        cols
    ```

    We can be visualize the elements of the nonscalar structure array like this

    ![nonscalar structure illustration](images/struct_illustration2.png){ width="250"}
   
### Accessing Field Content in a Structure Array

So, how do you get the data out? To get the data from the first element in the array, simply index the structure name, as follows:

```matlab linenums="1" title="Accessing content from the rows field in element 1 of the nonscalar structure"
img_info(1).rows
```

```matlab title="result"
ans = 
      25
```

If you do not include the index, then MATLAB returns the values from all the fields sequentially.

```matlab linenums="1" title="Accessing content from the cols field across all elements in nonscalar structure"
img_info.cols
```

``` title="result"
ans =

    50

ans =

   200
```

…Notice that the output is a comma-separated list, spitting out the contents, one  after the other, overwriting *`ans`* each time with the new content. This is similar to what happens when we access multiple cells in a cell array using the curly brackets.

To concatenate the output, you must include a concatenating special character (i.e. `[ ]`  or `{ }`):

```matlab title="Concatenating scalar content from the same field across all structure elements"
>>cols = [img_info.cols]
cols =

    50   200
```

This works for scalar content, like numbers. But for nonscalar content, like a character array, you need to use the curly brackets and package the data into a cell array.

```matlab linenums="1" title="Concatenating Character arrays from all structure elements"
filenames = {img_info.filename} % note use of curly brackets
```

```matlab title="result"
filenames = 

    'moonshot.jpg'    'apollo13.jpg'
```

…The above syntax extracts the filenames from the `filename` field across all elements of *img_info* and concatenates them into a new 1X2 cell array called *`filenames`*.

#### Challenge

=== "Question 1"

    Show the syntax to sum the values from rows field in *`img_info`*
=== "Answer 1"
    Show the syntax to sum the values from rows field in *`img_info`*:

    ```matlab linenums="1"
    sum([img_info.rows])
    ```

    ```matlab title="result"
    ans =

        125
    ```

    Without the square brackets, you would get a sum of 25. Why?
=== "Question 2"

    What happens when you use the Square Brackets to concatenate the content from the filename fields?
=== "Answer 2"
    What happens when you use the Square Brackets to concatenate the content from the filename fields?

    ```matlab linenums="1"
    [img_info.filename]
    ```

    ```matlab title="result"
    ans =

    'moonshot.jpgapollo13.jpg'
    ```

    You get the two filenames crammed into one character array

---

## Advanced Topic: Programmatically Accessing a Structure Field

*A somewhat complicated example*

Sometimes you want to access the fields in a structure programmatically, i.e. using a variable to indicate the field. To do so, you can use parentheses, as follows:

`structure_name.('name_of_field')`

Do not confuse this syntax with indexing an array. Notice that in this syntax the period immediate proceeds the parentheses. Inside the parentheses, the field name is entered as a character array or a variable containing a character array. For example:

```matlab
img_info.('filename')
```

### Creating a dialog to select a field name in a structure

If you would like to access the content from a structure after receiving user input, you could use the following programmatic steps:

First, get the field names from the *`img_info`* using the function **`fieldnames`**. This function returns all the field names in from a structure array as a cell array.

```matlab linenums="1" title="Get Structure Field names"
fld_names = fieldnames(img_info)
```

```matlab title="result"
fld_names = 

    'filename'
    'rows'
    'cols'
```

…Notice the output *`fld_names`* is a cell array.

We can plug this cell array into one of MATLAB's built-in dialog functions, **`listdlg`**. This function creates a dialog in which the user can select one element from the inputed cell array:

```matlab linenums="1" title="Create a list dialog for user input"
answer = listdlg('ListString',fld_names)
```

The **listdlg** function creates the following dialog window.

![][img-listdlg window]

[img-listdlg window]: images/listdlg-window.png

…Notice that the field names from *`img_info`* are listed in the dialog window. Also notice that you select one of the rows.

After you make your selection and you click 'OK', **`listdlg`** returns the index of the rows selected and assigns that value to `answer`. If you click "Cancel", **`listdlg`** sets `answer` to empty.

We can use the value  in `answer` to index the input cell array *`fld_names`*

```matlab linenums="1" title="Get selected field"
selected_field = fld_names{answer}
```

```matlab title="result"
selected_field =

rows
```

Then we can display the contents of the selected field from the *`img_info`* structure array using the following syntax:

```matlab linenums="1" title="Get Contents from selected field"
img_info.(selected_field)
```

```matlab title="result"
ans =

    25


ans =

   100
```

In the above example, the values from the *row* field from both elements of the structure array are displayed. However, if we indicate the index of the element, then we would get the result from the field in that element of the structure. In the following example, we indicate the second element of the structure array and get just one result.

```matlab linenums="1" title="Get contents from just one element in the structure array"
img_info(2).(selected_field)
```

```matlab title="result"
ans =

    100
```

[FIN](#overview). 🌳

<!--### Class Exercise Write a for loop that displays the field contents from img_info in the command window.-->