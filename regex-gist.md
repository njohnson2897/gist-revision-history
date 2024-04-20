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

In the second half of the expression we see four quantifiers as well: 

```
([a-z\.]{2,6})([\/\w \.-]*)*\/?$
```

The first is a {min, max} quantifier, indicating that the bracket expression it is connected to can have between 2-6 a-z characters.  The second and third are * quantifiers, which mean that the bracket and parentheses expressions that they are respectively attached to can occur 0 or more times.  In other words, the character parameters outlined in those expressions can be nonexistent or be as many characters long as necessary.   Lastly, we have another ? quantifier following the forward slash at the end of the expression.   Again, this indicates that the forward slash is optional.

### Grouping Constructs
Grouping constructs serve multiple purposes within a regular expression.  They are represented with open and close parentheses (  ), and much like their mathematical counterpart, they group the characters that are found within them.  Due to this grouping, a quantifier attached at the end of a grouping construct would apply to the whole group, as explained in the quantifier section.  It is important to note that, unlike bracket expressions, the characters represented within the construct are considered literal unless otherwise indicated.  This means that (abc) would be a search pattern that only matches with "abc" and not "cba", "ac" or "bc".  Further, (abc)? would mean that a string "abc" can occur 0 or 1 times, not that each of "a", "b", and "c" are optional.  The last point to note about these constructs is that they can be used to "capture" the data within them, meaning that when a matching process is complete, the data can be return for re-use in another manner.

In our regular expression we see four grouping constructs which I will separate with ~~~ in the following snippet:

```
(https?:\/\/)?   ~~~  ([\da-z\.-])   ~~~    ([a-z\.]{2,6})   ~~~   ([\/\w \.-]*)*
```
The point of the first construct is to group together the https:// portion  of the URL and assign the ? quantifier to make it optional.  The  second construct would represent the main content URL, namely everything before the .com.  This is likely grouped in order to capture it and make it available for re-use.  The  third represents the  .com, .net, .org, or whatever tag might end the URL.  The last one is grouped together possibly to capture the search parameters following the .com but also to assign the *  (0 or more instances) identifier to  the entire group, meaning that there could be 0 characters after .com or there could be hundreds.

### Bracket Expressions
Bracket expressions are parameters that we place inside of square brackets [ ].  They represent ranges of characters that we might be searching for and are not literal like grouping constructs.  In other words [abc] will search for any string that contains an "a", "b", or "c", not only strings that are literally "abc".  More commonly, hyphens are used to express ranges of characters, such as [a-zA-Z] to match all letters.  They can be inverted with carets ^, thus [^a-zA-Z] would search for all strings that do not contain any letters at all.

In our URL regex we have three brackets expressions, which I will reprint below:

```
[\da-z\.-]     [a-z\.]       [\/\w \.-]
```
The first uses character classes and character escapes that will be discussed later, but essentially means that this expression will match with any string that contains a digit, a lowercase letter, a period, or a hyphen.  The second simply includes lowercase letters and a period.  The last one will match with any string that contains a forward slash, any uppercase or lowercase letter or digit, or a period or hyphen.

### Character Classes
Character classes are means of simplifying regular expressions so that you do not have to list out every possible letter, digit, or symbol that you might be attempting to match.  Some common classes include \d for any digit 0-9, \w for any letter or digit, including both lower and upper case, and \s which matches with whitespace.  Like with bracket expressions, you can logically invert these classes by using upper case letters in the class.  For example, \D would match with any string that contains no digits at all.

In the URL regex, we see two character classes called:

```
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
```
The first is seen in the second grouping construct.  The expression utilizes a \d within a bracket expression to indicate that that portion of the string might contain any digit.  The second is the \w found in the final bracket expression.  This is meant to show that the search parameters following the .com might contain any digit, or upper or lower case letter.

### The OR Operator
Regular expressions can utilize an OR operator, represented by a pipe |, to add additional logic to the parameters.  ORs can be used to make grouping constructs more flexible while still utilizing the capturing benefit of the constructs.  For example, (a|b|c) would no longer be a strict match for only the string "abc" but now acts more like [abc] while still capturing the  matched data.  However, there are no OR operators within this URL regex.

### Flags
Flags are used to define additional functionality or limits of a regular expression.  They are found after the forward slash that ends a regex.  The most common flags are "g", "i", and "m", which indicate that the regex should be a global, case-insensitive, or multi-line search, respectively.  There are also no flags in this URL regex.

### Character Escapes
Character escapes are used when you would like to add a search parameters of a character that also has an inherent regex definition already.  For example, a period . represents a character class that matches with any character at all, be it letter, digit, symbol, etc.  However, if you would like to add a period into your bracket expression, you can use a character escape,  initiated with a backslash, to allow the character to "escape" its regex definition.  For example, \. in a bracket expression no longer refers to any character at all but instead simply the actual period . character.

There are multiple character escapes found in the URL regex, which I will reprint below:

```
\/\/      \.      \.        \.          \/          \.        \/
```
While there are multiple instances, there are really only two types of escapes here.   The first is for the forward slash /, which typically begin and end regular expressions.  However, because actual forward slashes are quite common in URLs, we use the character escapes to include them in the bracket expressions.  The second is for the period . character, the reasoning for which I outlined in the paragraph above.  Periods are also quite common in URLs, so we must use escapes to avoid triggering  their inherent regex meanings.

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
