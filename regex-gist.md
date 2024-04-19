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

Regular expressions are always contained by forward slashes to indicate the beginning and end of the expression.  They can be made up of a variety of components, including anchors, quantifiers, grouping constructs, bracket expressions, etc.  These components all add or qualify certain parameters within the expression to further specify the search pattern of the expression.  In the sections below, I will explain what each type of component can do and how they operate within the example regular expression above.

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
Anchors are regex elements that signify positioning of the characters that either follow or precede them.  In other words, anchors indicate where the string that they might match would begin or end.  The two most common anchors are the caret "^" to mark the beginning of the string pattern and the dollar sign "$" to mark the end.  There is also the \b anchor to indicate a "word boundary", namely the end or beginning of a word or grouping of characters within the string as a whole.

In our example, we can see two anchors, a caret ^ and a dollar $, used to indicate that the URL will match all of the parameters that follow the caret and precede the dollar sign. 

```
/^ . . .  .  . . . . . . .  . $/
```
Put another way, all of the search parameters necessary for matching a URL are contained within the caret and dollar sign.

### Quantifiers
Quantifiers are components that indicate how many characters of a certain type you are searching for.  Because they do not provide any information about the type of character, they are typically attached to another kind of component, such as a character class, a component which will be explained later.  There are a variety of quantifiers: curly brackets can be used to indicate a minimum and maximum value, {min, max}, a minimum value, { min, }, or a specific value, { value }. There are also symbols that indicate specific quantities, such as * for a pattern that occurs 0 or more times, + for 1 or more times, and ? for a pattern that either doesn't occur or only occurs once. 

We see many examples of quantifiers in our URL matching regex. In the first portion of the expression, we can see three:

```
^(https?:\/\/)?([\da-z\.-]+)
```

The three quantifiers are the two question marks and the + at the end.  As stated above, ? indicates that the preceding character may occur 0 times or only once.  It is first attached to the "s" at the end of https.  This means that, due to the ?, this expression will match  with a URL that begins with http ("s" occurs 0 times), or https ("s" occurs 1 time).

There is a second question mark that follows the first closing parenthesis.  The parentheses group everything within, as will be discussed further in following sections.  As such, the ? that follows that closing parenthesis refers to everything contained within the parentheses.  Consequently, this regex will match with a string that begins with "http(s)://" or that doesn't begin with "http(s)://".  In other words, the http(s):// at the beginning of the URL is completely optional, and the string will be recognized as a URL with or without it.

Lastly, there is a + at the end of this whole portion of the expression.  It follows a closing square bracket, which, similarly to the parentheses we've seen, groups the parameters that precedes it up until the square brackets are opened.  Thus, the + is attached to the entire phrase [\da-z\.-].  Bracket expressions will be covered later, but suffice it to say now that the the content of the brackets indicates that what follows the https:// can contain digits, lower case letters, periods, or hyphens. The  + quantifier attached to this phrase means that the string must contain 1 or more of these characters.  To summarize "1abc", "abc", "123-", "-" etc. would match, but "A13-" would not, because the regex does not include capital letters.

### Bracket Expressions

### Grouping Constructs

### Character Classes

### The OR Operator

### Flags

### Character Escapes

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
