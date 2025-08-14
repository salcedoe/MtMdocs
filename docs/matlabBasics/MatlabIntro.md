# Muddling Through MATLAB

*The No Good, Very Bad, MATLAB User Guide You Never Wanted*

So, you're being forced to learn computer programming. Don't worry. It's not that bad once you get the hang of things.

!!! question "Let me ask you a question:"

    - Can you read?
    - Are you good at copying and pasting?
    - Can you point and click on things?
    - Do you know how to make a list of instructions?

Alright, that's more than one question, but if you can do most of the above then you too can barely learn to program.

Learning to program is a lot like learning a foreign language. You start completely lost. Then, slowly you start to understand a word here and there. And then suddenly, it clicks, and you're smoking and chatting away with your new friends in Italy.

## So, what is programming, anyway?

Computer programming is primarily a written language where you write a sequence of words and phrases to tell a computer what to do. And like all written languages, there are specific rules on the order of the words, the spacing, and the punctuation. These rules are called **syntax**. And syntax matters, ***critically***. Turns out that your English teacher was right.

The biggest hurdle to learning computer programming is getting the syntax *just* right. This is also the source of most frustration.

!!! example "Violent Syntax"
    Consider the following fairly innocuous sentence:

    > The Panda eats shoots & leaves.

    ![img-name](images/panda-diet_feat.jpg){ width="250"}

    …Here, the panda is enjoying a nice, leafy meal.

    But the meaning of the sentence changes violently with the addition of a single comma:

    > The Panda eats, shoots & leaves

    ![Tactical Panda](images/tactical-panda.png){width="200"}

    …Now the Panda is a wanted criminal and on the run. 
    
    *See [Lynne Truss's](https://read.amazon.com/kp/embed?asin=B000OIZSVY&preview=newtab&linkCode=kpe&ref_=cm_sw_r_kb_dp_p4AtDbWSS3EKY) book "Eats, Shoots and Leaves" for more such delightful examples in the English language.*

Bottom line: Computers are dumb and don't get nuance. If you say something just a little wrong, the programming language will fail until you state your command in the precise way that the computer was expecting. It's kind of like using OK Google, Siri, or Alexa, but instead of just shouting at an inanimate object, you are also pounding on the keyboard.

## The MATLAB Programming Language

In this guide, we will cover the fundamentals of MATLAB as we learn computer programming. MATLAB stands for MATrix-LABoratory. A matrix is a data type similar to a spreadsheet. Matrices are in fact the main data structure of digital images (We'll get into what a data structure means soon, but for now just roll with it). MATLAB is very good at handling matrices, which is one of the reasons why we are learning this language in the first place. MATLAB also has excellent documentation and a great integrated development environment that simplifies the learning process.

Now, you may hear some people malign the choice of MATLAB. *Why aren't you learning Python, Java, or some other flavor of the month?* Ignore these people. They likely don't have an academic license for MATLAB like we do. And MATLAB includes some nice tools to help soothe the pain of learning programming. Plus, it really doesn't matter what language you use to learn computer programming because, in the end, it is all just syntax. Just like it is easier to learn Italian after learning how to speak Spanish, learning MATLAB makes it easier to learn other programming languages. And, beyond MATLAB, learning programming will give you the foundation to understand the digital underpinnings of other data analysis software so that when you learn new software, even if there is no programming involved, you will be primed to more quickly understand how the software works and how to get the most out of that software.

!!! abstract "What so bad about Excel?"

    One of the reasons that we are learning a programming language like MATLAB is that spreadsheets, like those created by Excel, are infamously known to be riddled with errors, especially complex spreadsheets with lots of formulas. Such formulas are hard to track, especially when there are a lot of cells and it's easy to make mistakes. Even worse, just opening an excel file can create issues. Consider the example discussed in [this article](https://theconversation.com/excel-autocorrect-errors-still-plague-genetic-research-raising-concerns-over-scientific-rigour-166554), which discusses the perils of Autocorrect in Excel spreadsheets for gene research. Apparently, just opening an excel file can activate the autocorrect "feature", which will dutifully go through all of the cells and change perfectly good gene names, like MARCH1 to a date. The issue was so bad that they had to rename the gene name to avoid this problem.

## User Guide Conventions

As we move forward, we will assume that you are already familiar with the [MATLAB Desktop](https://www.mathworks.com/help/matlab/learn_matlab/desktop.html), especially the Command Window (and command line), the Workspace, and the Current folder. A lot of this information and more can be found in the freely available [MATLAB Onramp tutorial](https://matlabacademy.mathworks.com/details/matlab-onramp/gettingstarted), which you should definitely complete before going forward with this resource. You should also know what a live script is and [how to create one](https://www.mathworks.com/help/matlab/matlab_prog/create-live-scripts.html).

That's right. You're going to have to learn some of this stuff on your own.

But you can handle it.

!!! warning
    The following contains actual programming concepts. The learning starts now.

This guide is broken up into different learning modules that cover one specific programming concept (like Variables or Functions).

Throughout the modules, the following conventions are used:

- MATLAB **`functions`** and *`variables`* are bold or italicized, respectively.

- Code blocks that contain MATLAB code are lightly shaded, as follows:

```matlab linenums="1"
version
```

…The command **`version`** just reports the current version of MATLAB. Since there is just one line of code, there is just one line number: `1`.

Many of these examples are designed to be copied directly into MATLAB, so you can try programming on your own. Notice if you hover over the lightly shaded area, a copy icon will appear. If you click on the icon, the code will be copied to your clipboard and you can then just paste into MATLAB

For clarity, I will often include the output that is spit out after you enter a command in MATLAB. This code **should not be copied or pasted**—you'll probably get an error if you do. So, I will differentiate the output text in two ways:

1. The title of the code block will often be "result".
2. There will be no line numbers on the left-hand side of the code block.

For example, the following code block contains the output found in the command line after you execute the `version` command above.

!!! warning "Don't copy or paste code that doesn't have line numbers."
    ```matlab title="result"
    ans =

        '24.1.0.2537033 (R2024a)'
    ```
    Notice that the above code block is titled **result** and there are no line numbers on the left-hand side.

Try it now. Copy the **`version`** command above and paste it into the Command Line in MATLAB. After you hit enter you should get an output similar to what I got (It may be different if you are using a different version of MATLAB).
