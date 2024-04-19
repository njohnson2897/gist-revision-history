# Regex for Matching a URL

In this gist I will be explaining the basic concepts behind regular expression: what they look like, what they do, how they can be used, and some specific examples of commonly used regular expression patterns.

Regular expression, or regex, is a piece of code that specifies certain parameters to be used as search criteria for matching with characters within a body of text.  Much like you might use Control + F in a word document to find how many times and where you utilize a certain word, a developer can use a regex to pinpoint where a certain pattern of characters shows up in a text that they are working with.  For this reason, they can be  helpful to developers in a number of ways.  

First, they can be used as an extremely adaptable document search function.  Rather than simply searching for certain words, regex allows you to search for endless combinations of characters, such as a digit, followed by anywhere from 3-6 non-digit characters, all of which comes at the beginning of a new line of text.

The other most common usage of regex would be to validate certain user inputs.  For example, a webpage might have a form in which users are meant to input a phone number and email address to sign up for an account.  Because phone numbers and email addresses all share certain properties (e.g. all email addresses containing an @ followed by a domain name), regex can be used to validate that the string inputted by the user is, in fact, the proper syntax for an email adress or phone number. 

## Summary

The remainder of this gist will be looking at a specific regex that can be used to search for a validate that a string is a URL.  The following is what this sort of regular expression looks like:

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```

Regular expressions can be made up of a variety of components, including anchors, quantifiers, grouping constructs, bracket expressions, etc.  These components all add or qualify certain parameters within the expression to further specify the search pattern of the expression.  In the sections below, I will explain what each type of component can do and how they operate within the example regular expression above.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

### Quantifiers

### Grouping Constructs

### Bracket Expressions

### Character Classes

### The OR Operator

### Flags

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
