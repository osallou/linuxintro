# Grep and regular expressions

## what is it

Regular expressions are similar to the wildcards that we looked in
previous sections.
They allow us to create a pattern. They are a bit more powerful however.
Re's are typically used to identify and manipulate specific pieces of
data.
we may wish to identify every line which contains an email address or
a url in a set of data.

Regular expressions are not linux specific and used in many programming languages.

## eGrep

egrep is a program which will search a given set of data and print every
line whichcontains a given pattern.
It is an extension of a program called grep.

    egrep [command line options] <pattern> [path]


    $ egrep 'mellon' mysampledata.txt
    Mark watermellons 12
    Oliver rockmellons 2

The basic behaviour of egrep is that it will print the entire line for
every line which contains a string of characters matching the given pattern.
This is important to note, we are not searching for a word but a string of
characters.

Sometimes we want to know not only which lines matched but their line
number as well.

    $ egrep -n 'mellon' mysampledata.txt
    3:Mark watermellons 12
    11:Oliver rockmellons 2

Or maybe we are not interested in seeing the matched lines but wish to
know how many lines did match.

    $ egrep -c 'mellon' mysampledata.txt
    2

## regular expressions reminder

* . (dot) - a single character.
* ? - the preceding character matches 0 or 1 times only.
* \* - the preceding character matches 0 or more times.
* + - the preceding character matches 1 or more times.
* {n} - the preceding character matches exactly n times.
* {n,m} - the preceding character matches at least n times and not more than m times.
* [agd] - the character is one of those included within the square brackets.
* [^agd] - the character is not one of those included within the square brackets.
* [c-f] - the dash within the square brackets operates as a range. In this case it means either the letters c, d, e or f.
* () - allows us to group several characters to behave as one.
* | (pipe symbol) - the logical OR operation.
* ^ - matches the beginning of the line.
* $ - matches the end of the line.

We'll start with something simple.
Let's say we wish to identify any line with two or more vowels in a row.
In the example below the multiplier {2,} applies to the preceding item which
is the range.

    $ egrep '[aeiou]{2,}' mysampledata.txt
    Robert pears 4
    Lisa peaches 7
    Anne mangoes 7
    Greg pineapples

Now you can play with different patterns...
