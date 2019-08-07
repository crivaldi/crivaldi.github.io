---
layout: post
title: String manipulation with sed and grep
subtitle: Some tips on using sed and grep
---
# String manipulation with sed and grep

What is string manipulation and why do we care about this? As biologists, or more generally as people interested in working with data, a lot of what we want to do will require us to manipulate many characters at the same time. By definition:

*   A **character** is class whose instances can hold a single character value.
*   A **string** is an _immutable_ class for working with multiple characters.

   Strings are information that we don't want to use for numerical calculations. DNA sequences, column or row names, and categorical/qualitative data values will generally be strings. You might want to remove the primers from a lot (like _a lot_) of sequences at the same time, or you might want to remove whitespaces from a dataset you found online. Most of our string manipulation is covered by the previous links that are tied in with the for loops - here are a couple of useful comics for some of those commands though. 'awk' is in some ways is its own programming language - it's very much worth learning, despite being a bit more complicated than sed or grep. ![](http://sites.nd.edu/crivaldi/files/2018/09/awk.jpg) ![](http://sites.nd.edu/crivaldi/files/2018/09/sed.jpg) ![](http://sites.nd.edu/crivaldi/files/2018/09/grep.jpg) [https://www.hackerearth.com/practice/algorithms/string-algorithm/basics-of-string-manipulation/tutorial/](https://www.hackerearth.com/practice/algorithms/string-algorithm/basics-of-string-manipulation/tutorial/) [https://pythonforbiologists.com/printing-and-manipulating-text/](https://pythonforbiologists.com/printing-and-manipulating-text/)
