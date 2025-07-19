## Grouping Variables

Up to this point, we have been plotting entire columns of data. Sometimes though we need to separate the data in a column into distinct groups. We can group this data using grouping variables.

Consider the following columns in our dataset

```matlab
T.MDT = datetime(T.MDT); % good for time data
T.Events = categorical(T.Events); % good for statistical organization
T.Events = addcats(T.Events,'none'); % add a category of none
T.Events(isundefined(T.Events)) = 'none'; % set all undefined events to the category of none
categories(T.Events) % list the categories found in events
```

Consider for example our events column.

Using grouping variables, we can group the different rows of the table into different categories, isolating these subsets of data. Notice that in our table we have columns of numbers, such as temperature, dewpoint, humidity, and windspeed, and columns of identification, such as date (MDT) and event (e.g., rain, snow, etc.). The identifying data are also known as grouping variables and can be used to group rows into different categories.
These grouping variables are more useful when you typecast them to certain variable types, like datetime and categorical

### Bar Example 1: Bar Plot event counts

#### Bar Example 1: Clean up the data and group

The "Events" column of **`T`** contains categorical data---data that can easily be divided into groups.

To simplify plotting this data, we are going to convert this column to a categorical class:

```matlab linenums="1" title="Convert Events column to a categorical array"
T.Events = categorical(T.Events)
```

```matlab title="Contents of Event column"
ans = 

  30×1 categorical array

     <undefined> 
     <undefined> 
     <undefined> 
     Rain-Thunderstorm 
     Rain-Thunderstorm 
     ⋮
```

…As you can see, many rows contain the term `<undefined>`, while some contain an event, like 'Rain-Thunderstorm'.

For our purposes, we'll use `<undefined>` as an indicator that there was no weather event and we'll call this event `'none'`. We can convert `<undefined>` to `'none'` in the array as follows:

```matlab linenums="1" title="Replace undefined data"
T.Events(isundefined(T.Events)) = ('none') % replace all undefined data with 'none'
```

```matlab title="result"

  30×1 categorical array

     none 
     none 
     none 
     Rain-Thunderstorm 
     Rain-Thunderstorm 
```

#### Bar Example 1: Count Events

To plot our bar plot, we first need to count up the number of each event (or group). The function **`groupsummary`** simplifies this nicely:

```matlab linenums="1"
s = groupsummary(T,"Events")
```

```matlab title="result"
s =

  6×2 table

           Events            GroupCount
    _____________________    __________

    Fog                           1    
    Fog-Rain                      2    
    Fog-Rain-Thunderstorm         2    
    Rain                          4    
    Rain-Thunderstorm             7    
    none                         14    
```

…**`groupsummary`** returns a table, *`s`*, with the data that we need for the next step. And importantly, this data is already sorted by count.


#### Bar Example 1: Plot Event Counts

Now we are ready to plot our data. The following code creates a bar plot and adds a title, an x- and a y-label. It also changes the transparency of the bars, so you get a nicer shade of blue.

```matlab linenums="1" title="Plot Event Counts as a Bar Plot"
x = s.Events;
y = s.GroupCount;

hb = bar(x,y); % notice the two inputs

hb.FaceAlpha = 0.5; % increase transparency of plot (nicer shade of blue)

% axis formatting
ylabel("Number of days")
xlabel("Weather Event","FontWeight","bold")
title("Denver - September 2013")
ylim([0 17]) % increase the limits on the y-axis
```

…Notice since *`x`* is a categorical array, we got the event labels at the bottom of the bar plot. (1)
{.annotate}

1. The function **`bar`** does not accept a string or a cell array as an input for *`x`* — it has to be a categorical array for this to work.

![Bar Plot Event Counts][bar-ev-count]{width=450px}

>Notice in this bar plot, that the counts of the events have been sorted from fewest to most. This makes the data much easier to interpret. On the left, we se that there were very few days of fog, while on the right, we see that on a majority of days, nothing of note happened ('none').

[bar-ev-count]:images/bar-event-counts.png

### Example 2: Horizontal Bar Plot

The function **`barh`** operates exactly like **`bar`**, but produces horizontal bars, as follows:

```matlab linenums="1"
hb = barh(x,y);

hb.FaceAlpha = 0.5; % increase transparency of plot

% axis formatting
xlabel("Number of days")
ylabel("Weather Event","FontWeight","bold")
title("Denver - September 2013")
% ylim([0 17]) % increase the limits on the y-axis
xlim([0 15])
```

![Horizontal Bar Plot][bar-ev-count-sorted-hz]{width=450px}

[bar-ev-count-sorted-hz]:images/bar-event-counts-hz.png  

…And now our bar plot is horizontal. Notice that we had to input the correct data in the correct labeling functions and we had to use **`xlim`** instead of **`ylim`**.