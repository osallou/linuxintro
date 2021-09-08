# Filters

A filter, in the context of the Linux command line,
is a program that accepts textual data and then transforms it in a particular
way.

Filters are a way to take raw data, either produced by another program,
or stored in a file, and manipulate it to be displayed in a way more suited to
what we are after.

These filters often have various command line options that will modify their
behaviour so it is always good to check out the man page for a filter to see
what is available.

In the examples below we will be providing input to these programs by a file
but in the section [Piping and Redirection](12_piping.md) we'll see that we may provide input via other means that add a lot more power.

## setup

We suppose we have a file named [mysampledata.txt](mysampledata.txt) with some space delimited content.

## head

Head is a program that prints the first so many lines of it's input.
By default it will print the first 10 lines but we may modify this with a
command line argument.

head [-number of lines to print] [path]

    $ head mysampledata.txt
    Fred apples 20
    Susy oranges 5
    Mark watermellons 12
    Robert pears 4
    Terry oranges 9
    Lisa peaches 7
    Susy oranges 12
    Mark grapes 39
    Anne mangoes 7
    Greg pineapples 3


    $ head -4 mysampledata.txt
    Fred apples 20
    Susy oranges 5
    Mark watermellons 12
    Robert pears 4


## tail

Tail is the opposite of head.
Tail is a program that prints the last so many lines of it's input.
By default it will print the last 10 lines but we may modify this with a
command line argument.

    tail [-number of lines to print] [path]

    $ tail mysampledata.txt
    Mark watermellons 12
    Robert pears 4
    Terry oranges 9
    Lisa peaches 7
    Susy oranges 12
    Mark grapes 39
    Anne mangoes 7
    Greg pineapples 3
    Oliver rockmellons 2
    Betty limes 14

## sort

Sort will sort it's input, nice and simple.
By default it will sort alphabetically but there are many options available
to modify the sorting mechanism.
Be sure to check out the man page to see everything it may do.

    sort [-options] [path]

    $ sort mysampledata.txt
    Anne mangoes 7
    Betty limes 14
    Fred apples 20
    Greg pineapples 3
    Lisa peaches 7
    Mark grapes 39
    Mark watermellons 12
    Oliver rockmellons 2
    Robert pears 4
    Susy oranges 12
    Susy oranges 5
    Terry oranges 9


## nl

nl stands for number lines and it does just that.

    nl [-options] [path]

    $ nl mysampledata.txt
    1 Fred apples 20
    2 Susy oranges 5
    3 Mark watermellons 12
    4 Robert pears 4
    5 Terry oranges 9
    6 Lisa peaches 7
    7 Susy oranges 12
    8 Mark grapes 39
    9 Anne mangoes 7
    10 Greg pineapples 3
    11 Oliver rockmellons 2
    12 Betty limes 14

## wc

wc stands for word count and it does just that (as well as characters and lines.
By default it will give a count of all 3 but using command line options we may limit it to just what we are after.

    wc [-options] [path]

    $ wc mysampledata.txt
    12 36 197 mysampledata.txt

## cut

cut is a nice little program to use if your content is separated into fields (columns) and you only want certain fields.

    cut [-options] [path]

In our sample file we have our data in 3 columns, the first is a name,
the second is a fruit and the third an amount.
Let's say we only wanted the first column.

    $ cut -f 1 -d ' ' mysampledata.txt
    Fred
    Susy
    Mark
    Robert
    Terry
    Lisa
    Susy
    Mark
    Anne
    Greg
    Oliver
    Betty

cut defaults to using the TAB character as a separator to identify fields.
In our file we have used a single space instead so we need to tell cut to use that
instead.

The separator character may be anything you like, for instance in a CSV file the
separator is typically a comma ( , ).

This is what the -d option does (we include the space within single quotes so it knows
this is part of the argument).
The -f option allows us to specify which field or fields we would like.
If we wanted 2 or more fields then we separate them with a comma as below.

    $ cut -f 1,2 -d ' ' mysampledata.txt
    Fred apples
    Susy oranges
    Mark watermellons
    Robert pears
    Terry oranges
    Lisa peaches
    Susy oranges
    Mark grapes
    Anne mangoes
    Greg pineapples
    Oliver rockmellons
    Betty limes

## sed

sed stands for Stream Editor and it effectively allows us to do a search and replace
on our data. It is quite a powerful command but we will use it here in it's basic format.

    sed <expression> [path]

A basic expression is of the following format:

    s/search/replace/g

The initial s stands for substitute and specifies the action to perform
(there are others but for now we'll keep it simple).
Then between the first and second slashes ( / ) we place what it is we are searching
for (can be regular expression).
Then between the second and third slashes, what it is we wish to replace it with.
The g at the end stands for global and is optional.
If we omit it then it will only replace the first instance of search on each line.
With the g option we will replace every instance of search that is on each line.

Let's see an example. Say we ran out of oranges and wanted to instead give those people bananas.

    $ sed 's/oranges/bananas/g' mysampledata.txt
    Fred apples 20
    Susy bananas 5
    Mark watermellons 12
    Robert pears 4
    Terry bananas 9
    Lisa peaches 7
    Susy bananas 12
    Mark grapes 39
    Anne mangoes 7
    Greg pineapples 3
    Oliver rockmellons 2
    Betty limes 14

Sed, by default, does not modify input file. Using "-i" option, input file is modified.


## uniq

uniq stands for unique and it's job is to remove duplicate lines from the data.
One limitation however is that those lines must be adjacent (ie, one after the other). (sometimes this is not the case but we'll see one way we can fix this in [Piping and Redirection][12_piping.md]).

    uniq [options] [path]

Let's say that our sample file was actually generated from another sales program
but after a software update it had some buggy output.

    $ cat mysampledata.txt
    Fred apples 20
    Susy oranges 5
    Susy oranges 5
    Susy oranges 5
    Mark watermellons 12
    Robert pears 4
    Terry oranges 9
    Lisa peaches 7
    Susy oranges 12
    Mark grapes 39
    Mark grapes 39
    Anne mangoes 7
    Greg pineapples 3
    Oliver rockmellons 2
    Betty limes 14

No worries, we can easily fix that using uniq.

    $ uniq mysampledata.txt
    Fred apples 20
    Susy oranges 5
    Mark watermellons 12
    Robert pears 4
    Terry oranges 9
    Lisa peaches 7
    Susy oranges 12
    Mark grapes 39
    Anne mangoes 7
    Greg pineapples 3
    Oliver rockmellons 2
    Betty limes 14

## Others

Here are two other programs that are worth investigating if you want to take your knowledge even further.
They are a quite powerfull but also more complex than the programs listed above.

* awk
* diff