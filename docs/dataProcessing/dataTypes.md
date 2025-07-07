# Data Types

Data can be broadly categorized into two types:

1. **Quantitative**. Also known as Numeric, these data are used to count or measure something. Their values are stored in various numeric classes of MATLAB, including floating-point types (such as double and single) and integer types (such as uint8, uint16, int32, etc.).
2. **Qualitative**. Also known as Categorical, these data are used to describe something using a label like Male or Female, or Good or Bad. In MATLAB, qualitative data can be stored as logical, string, or [categorical arrays (see below)](#categorical-arrays), depending on the nature of the categories.

```mermaid
graph TD
    DATA:::data --> Num[Numbers];
    DATA --> Cat[Categories];
    Num --> Disc[Discrete];
    Num --> Cont[Continuous];
    Cat --> Nom[Nominal];
    Cat --> Ord[Ordinal];
    Cont --> Int(interval)
    Cont --> Rat(ratio)
    Rat --> RatX(speed, height, weight)
    Int --> IntX(Temp, 12-Hour Clocks)
    IntX --> MatFloat(datetime, single, double)
    RatX --> MatFloat
    Disc --> Whole(Whole Numbers)
    Whole --> WholX(Counts, Ratings,
     Images)
    WholX --> MatInt(uint8, uint16, etc.)
    Nom --> NomDesc(No Order)
    Ord --> OrdDesc(Ordered)
    NomDesc --> NomX1(Male, Female)
    NomDesc --> NomX2(Colors)
    OrdDesc --> OrdX(Beginner,
     Intermediate,
     Advanced)
    NomX1 --> MatCat[string, categorical]
    NomX2 --> MatCat
    OrdX --> MatCat
    class Num,Disc,Whole,WholX,Cont,Int,IntX,Rat,RatX nums
    classDef nums fill:#5DADE2  
    classDef data fill:#F39C12
    class MatFloat,MatInt,MatCat mats
    classDef mats fill:#48C9B0

```

!!! abstract "Categorizing Data"

    **Numeric Data** can be classified into Discrete or Continuous classes. 
    
    - **Discrete** numbers are whole numbers or integers.
    
    - **Continuous** numbers have an infinite number of possible values between whole numbers, like `1.2` or the value of $\pi$. In statistics, Continuous numbers can be further classified into **Interval** and **Ratio** values, depending on whether they have a true absolute zero point (absence of value). The presence or absence of a true zero affects the types of mathematical operations you can perform and the conclusions you can draw from the data. For example, you can't say 20°C is twice as hot as 10°C (interval), but you can say 20kg is twice as heavy as 10kg (ratio).

        <div class="annotate" markdown>

        - **Interval Numbers**, like Temperature (1) or Time on a clock, do not have an absolute zero reference. For example, 0 C˚ or 0 F˚ Temperature, does not mean no temperature, it simply one value in a range of values. Similarly, 0:00 does not mean the absence of time, it just means midnight. In fact, to handle time values, MATLAB came up with the [**`datetime`**](https://www.mathworks.com/help/matlab/ref/datetime.html){target="_blank"} data type.
        

        - **Ratio Numbers**, by comparison, do have an absolute zero reference. For example,  a height of 0 means the absence of height and a weight of 0 means absence of any weight, so measurements like height, weight, speed, are all Ratio Numbers. By the way, time measured in seconds would also be a Ratio number, since in this scenario 0 seconds means the absence of seconds.

        </div>
    

        1. unless you're dealing with Kelvin
       

    **Categorical Data** can be further classified into Ordered (Ordinal) or Non-ordered (Nominal) categories. Ordinal categories are categories with an implied order, such as Beginner, Intermediate, or Advanced. Nominal categories do not have an implied order, e.g. Male and Female.

## Categorical Arrays

To handle Qualitative Data, MATLAB created the [`categorical`](https://www.mathworks.com/help/matlab/categorical-arrays.html) variable type. Categorical arrays operate similar to string arrays, but they have built-in functions for statistical uses.

Consider the following string array.

```matlab linenums="1" title="Create String array"
sex = ["Male" "Male" "Female" "Female" "Male" "Female"] % create string array
```

```matlab
sex = 

  1×6 string array

    "Male"    "Male"    "Female"    "Female"    "Male"    "Female"
```

We can easily convert this string array into a categorical array using the function **`categorical`**

```matlab
sex = categorical(sex) % typecast to categorical
```

…Here we just overwrite the string array with its categorical version

```matlab
sex = 

  1×6 categorical array

     Male      Male      Female      Female      Male      Female 
```

And that's it. *`sex`* is now a categorical array. You can do a lot of the same things with a categorical array that you can do with a string array

```matlab linenums="1" title="Create logical array from a categorical array"
la = sex == "Male" % logical array
```

```matlab
la =

  1×6 logical array

   1   1   0   0   1   0
```

…Here we create a logical array from the relation operation "sex is equal to Male"

Categorical also has a lot of built-in functions, designed to make data analysis easier. The function **`categories`** returns the categories (or group names) in a categorical array

```matlab linenums="1" title="Get Categories"
categories(sex) % return categories
```

```matlab
ans =

  2×1 cell array

    {'Female'}
    {'Male'  }
```

…There are two categories: Female and Male

And you can use the function **summary** to report the count of each category in the array

```matlab linenums="1" title="Summary"
summary(sex) % rturns category count
     Female      Male 
     3           3    
```

### Creating Ordinal Data

If you have ordinal data, you still use the  **`categorical`** function, but with a couple of additional inputs.

```matlab linenums="1" title="Create Ordinal Categorical Array"
level = ["Advanced" "Advanced" "Beginner" "Intermediate" "Advanced" "Beginner"] % create string
level = categorical(level,{'Beginner','Intermediate','Advanced'},Ordinal=true) % typecast to ordinal
```

…Here, the second input into **`categorical`** is the category names in the order that you want. The third input sets Ordinal to true.

And we get an ordinal categorical array that looks very similar to just a categorical array.

```matlab
level = 

  1×6 categorical array

     Advanced      Advanced      Beginner    Intermediate  Advanced      Beginner     
```

The main differences is that when you call a function like  **`summary`**…

```matlab
summary(level)
```

```matlab
     Beginner      Intermediate      Advanced 
     2             1                 3       
```

…the results are reported in the order of the ordinal categories (and not in alphabetical order)

### Transforming Numeric Data into Qualitative Data

Sometimes the raw data comes in as numeric, when what you actually want is categorical.

Consider the following numeric array

```matlab
ratings = [3 3 2 1 3 2 1 1 1 2]
```

These numbers actually represent three different categories

1. Terrible
2. Meh
3. Awesome

To replace the numbers with the category labels, you enter the following into **`categorical`**:

```matlab
ratings = categorical(ratings,[1 2 3],{'Terrible','Meh','Awesome'},Ordinal=true)
```

…notice here that the second input is the rating categories as numbers, while the third input is the ratings categories as labels. The fourth input turns Ordinal on.

And you get…

```matlab
ratings = 

  1×10 categorical array

  Columns 1 through 5

     Awesome      Awesome      Meh      Terrible      Awesome 

  Columns 6 through 10

     Meh      Terrible      Terrible      Terrible      Meh 
```

…a categorical array with all the correct categories included.

And these categories show up in the summary:

```matlab
summary(ratings)
     Terrible      Meh      Awesome 
     4             3        3   
```
