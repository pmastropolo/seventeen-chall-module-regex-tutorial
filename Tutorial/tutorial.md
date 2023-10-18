# Regex Tutorial Module Seventeen Email Validation

Understanding Email Validation with Regular Expressions

## Summary

Regular expressions (often shortened to "regex") are a powerful tool for text processing. In this tutorial, I will explain the process of email validation using Regular Expressions. Hopefully, this tutorial, will help guide you on using regular expressions to match and validate email addresses. I will be going over, what a Regex is, anchors roles in defining the start and end points of patterns, Quantifiers, which dictate frequency of pattern repetitions, OR Operator, the power to choose between patterns. Also going over boundaries, ensuring you catch complete words, and not just parts, Look-Ahead and Look-Behind, to peek around main search.

### Regex To Validate Email Addresses:

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

## Table of Contents

- [What is a Regex](#what-is-a-regex)
- [TLD](#tld--top-level-domain)
- [Breakdown](#breakdown)
- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Sources](#sources)

## Regex Components

### What is a Regex?

You may be asking yourself, well what is a regex .. or regular expression?
A regex, or regular expression, is a sequence of characters that defines a specific search pattern.
It's a way to find patterns in text. 
You tell it what pattern you're looking for in a text, and it'll help you find it. 
It's like giving a detective a clue to find something for you.

### Why use it?

Let's say you have a big book and you want to find all the times they mention the word "pizza". Instead of reading the whole book, you could use a regex to quickly point out all the "pizza" spots. It saves time and makes things easier!

Here are some other examples of regexes:

Matching a Hex Value – /^#?([a-f0-9]{6}|[a-f0-9]{3})$/
Matching a URL – /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
Matching an HTML Tag – /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/

### Breakdown

Breaking down the Email Validation regex:

`/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

^ and $             : anchors that ensure entire string is matched.

([a-z0-9_\.-]+)     : captures username portion of email address. Allows lowercase letters, numbers,            underscore, dot, and hyphen in username. The + quantifier ensures that there is at least one character.
@ matches the at symbol

([\da-z\.-]+) captures one or more lowercase letters, digits, dots, hyphens for domain name. The + quantifier ensures that there is at least one character.

\. matches the literal dot (.) after domain name. separates the domain name from the TLD.

([a-z\.]{2,6}) captures 2-6 lowercase letters, or dots, for TLD. TLD can be combo of lowercase letters (a-z) and dots (.) The "{2,6}" specifies that TLD should have a minimum length of 2 characters and a maximum length of 6 characters.

This pattern follows common structure for matching email addresses, where local part is followed by the at symbol and the domain part, separated by a dot.

### TLD ( Top-Level Domain )

TLD stands for Top-Level Domain.
It is the last part of a domain name in an URL, such as .com, .org, .net, etc
TLDs are used to categorize/identify websites based on their purpose/geographical location.

### Anchors

In Javascript, you can use regular expression anchors to specify that a match should start at the beginning of a string and end at the end of a string.
These show where patterns start and finish.
The regex starts with ^ and ends with $.
The ^ anchor represents the start of the input string, so it ensures that the matching starts right at the beginning of the email address. 
The $ anchor represents the end of the input string, so it ensures that the matching ends right at the end of the email address.
Using these anchors can help ensure that the whole email address is being validated and no additional characters are included before or after it.

Examples:

/^hello/      Matches any string that starts with "hello".
/^[\d]+/      Matches any string that starts with one or more digits.
/^[A-Za-z]+/  Matches any string that starts with one or more uppercase or lowercase letters.
/^.{3}/       Matches any string that starts with any three characters.

### Quantifiers

Quantifiers in regular expressions are used to specify the number of occurrences or repetitions of a particular character or group in a pattern.
Tells how many times a pattern shows up.
They are symbols that indicate how many times a character or group of characters should appear in a pattern.
They help define the minimum and maximum number of occurrences of a specific element.

Here are some commonly used quantifiers in the context of email validation:

* (asterisk): This quantifier means "zero or more" and allows a character or group to appear any number of times,
including not appearing at all. 
Example: [\w.%+-]* means that the previous element can occur zero or more times.

+ (plus): This quantifier means "one or more" & requires a character, or group, to appear at least once.
Example:  [\w.-]+ means that the previous element must occur one or more times.

? (question mark): This quantifier means "zero or one" and allows a character or group to appear either once or not at all.
Example:  ([a-z\.]{2,6})? means that the previous element can occur zero or one time.

{n} (curly braces): This quantifier allows you to specify an exact number of occurrences for a character or group. 
Example: [a-zA-Z]{2,} means that the previous element must occur at least two times,
while `[a-zA-Z]{2,6}` means it can occur between two to six times.

In the email matching regular expression example, the quantifiers used are:

+ plus sign quantifier specifies that the preceding pattern should match one or more times. 
Example: ([a-z0-9_\.-]+) means that the username part can have one or more lowercase letters, digits, underscores, dots, and hyphens.

{2,6} curly braces with a range specified inside them indicate that preceding pattern should match a specific number of times within given range. 
([a-z\.]{2,6}) means extension part of email address should have between 2-6 lowercase letters or dots. 

### OR Operator

The OR Operator is represented by the pipe symbol. Allows you to match either pattern on its left or pattern on its right. Provides a way to specify alternatives within pattern. Helps find this pattern OR that pattern.

Can be used to specify multiple options for a certain part of the email address.
Example: want to match email addresses that end with either ".com" or ".org"
use regex pattern `\.com|\.org` to specify these two options.
The main example regex doesnt utilize OR operator, meaning, it doesn't specify any alternative patterns for matching.

Example:
 /^(example1|example2)@gmail\.com$/
This pattern matches email addresses that end with either "example1@gmail.com" or "example2@gmail.com".

### Character Classes

Character classes, define a set of characters, of which only one needs to match at a time. Essentially, Groups of characters that you might be looking for in your text.They are typically denoted within square brackets [], but some common sets have shorthand notations.For instance, \d is a shorthand character class that matches any single digit from 0-9.

The regex /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ contains several character classes:

1. [a-z0-9_\.-]   Matches lowercase letters, numbers, underscores, dashes, and dots. It is used to match the username part of the email address.

2. [\da-z\.-]     Matches lowercase letters, numbers, dots, and dashes. It is used to match the domain name part of the email address.

3. [a-z\.]        Matches lowercase letters and dots. It is used to match the top-level domain part of email address.


Here are some common character classes:

\D: Matches any character that's NOT a digit.
Useful when filtering out numeric data from a string.
Example: In "Order #456", Order # matches \D\D\D\D\D\D.

\W: Matches any character that's NOT a word character.
Great for isolating special symbols or punctuation from textual data.
Example: In "Hello, World!", the comma and exclamation mark ,! match \W\W.

\s: Matches any whitespace character (spaces, tabs, line breaks).
Essential for detecting gaps in textual data or formatting breaks.
Example: Between "Hello" and "World" in "Hello World", there's a space that matches \s.

\S: Matches non-whitespace.
Finds solid chunks of data without breaks.

\w: Matches any word character, which includes the alphanumeric characters (letters and digits) and underscore (_).

. (dot): Matches almost any character, except newline characters (by default).
The wildcard of regex. Useful when the exact character isn't known, but its position is.
Example: "&" matches .

\d: Matches any digit from 0 to 9.
Often used when parsing strings that have numerical data embedded within them.
Example: In the string "Model X100", 100 matches \d\d\d.

You can also define custom character classes using square brackets:

[abc]  
Matches any single character that is either "a", "b", or "c".
Acts as an OR for individual characters.
Example: In "I love zebra and lynx.", z and x match [xyz].

[^abc]
Matches any character not listed.
Useful when avoiding specific characters.
Example: In "apple", ppl matches [^xyz]+.

[0-9]  
Matches any single digit, equivalent to \d.

[a-zA-Z]
Matches any single uppercase or lowercase letter.
Captures any English letter.

### Flags

Flags are small changes that make pattern search different.
They are denoted by a single letter.

Some commonly used flags are:

i : Case-insensitive matching. This flag allows regex pattern to match both uppercase & lowercase letters.
/example/i would match "example", "Example", "EXAMPLE", etc.
g : Global matching. This flag allows regex pattern to match multiple occurrences of the pattern within a string.
/example/g would match all occurrences of "example" in a given string.
m : Multiline matching. This flag enables regex pattern to match start & end of each line within a multiline string.
Without this flag, pattern would only match start & end of entire string.
s (Single Line Match): This flag allows dot (.) character to match newline characters as well.
Without this flag, dot matches any character except newline.

The main email example regex doesnt use any flags here.
Flags are optional and do not need to be included in every regex.

### Grouping and Capturing

Grouping and Capturing, is about, finding and saving parts of your pattern.
By grouping, you tell the pattern to focus on this part for me.
By capturing, its like saying, remeber this part i might need it later.

There are 3 capturing groups in the regex:

1. ([a-z0-9_\.-]+): Matches the username part of an email.
2. ([\da-z\.-]+): Matches the domain name.
3. ([a-z\.]{2,6}): Matches the domain extension, like '.com' or '.org'.

### Bracket Expressions

Let you make your own group of characters to search for.

[a-z0-9_\.-]: This matches lowercase letters, numbers, underscores, dots, and hyphens.
[\da-z\.-]: This matches digits, lowercase letters, dots, and hyphens.
[a-z\.]: This matches lowercase letters and dots.
    
In /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/ , bracket expressions are used to define pattern for matching an email.

[a-z0-9_\.-]    Matches any lowercase letter, digit, underscore, dot, hyphen
[\da-z\.-]      Matches any digit, lowercase letter, dot, hyphen
[a-z\.]         Matches any lowercase letter or dot
{2,6}           Specifies [a-z\.] be repeated between 2-6 times

### Greedy and Lazy Match

Two ways your pattern can grab text.
The + quantifier is greedy by default,
which means it will match as many characters as possible.

In main regex email example, there are no specific instances of greedy/lazy matches. The pattern itself is searching for a specific format of an email address, where:

([a-z0-9_\.-]+) matches one, or more, lowercase alphabets, numbers, underscores, dots, hyphens
([\da-z\.-]+) matches one, or more, alphanumeric characters, dots, hyphens, underscores
([a-z\.]{2,6}) matches sequence of lowercase alphabets/dots, with length between 2-6
All of these matches are considered greedy matches by default, meaning, they try to match as many characters as possible while still satisfying overall pattern. 

However, if you wanted to make a specific part of pattern lazy, you could use ? after quantifier.
Example: 
If you wanted to make, ([a-z0-9_\.-]+) lazy, you could modify it to ([a-z0-9_\.-]+?)
This would match as few characters as possible while still satisfying overall pattern.
You could apply the ? to other quantifiers in pattern to make them lazy, as needed.

### Boundaries

What are they?
Make sure your finding whole words, and not just parts.
Boundaries are positions in text that mark the beginning or end of a word. 
They are used in regex to distinguish whole words from parts of words.
No word boundaries (\b) are used in the main email regex.

Examples:
Pattern: \bcat\b
This pattern finds the word "cat", but only if it stands alone.
In "I have a cat", it finds "cat". But in "I love my caterpillar", it doesn't see anything because "caterpillar" is more than just "cat".

### Back-references

Ever wish you could use a "copy-paste" button while talking? 
In patterns, there's a trick for that! 
Back-references let you "copy" a piece of your pattern and "paste" it somewhere else.

Back-references, allow you to refer back to previously captured groups in the same pattern ... A way for you to use parts of your pattern again later.
They are essential in regular expressions to perform searches that involve entire words, ensuring that you don't match substrings within words.
The main email regex doesn't use back references.
They are used to ensure that the same sequence appears more than once.

Examples:

Pattern: (dog) \1
This pattern finds the word "dog", then "copies" it and looks for a "pasted" repeat. 
The \1 is like hitting the "paste" button.

Pattern: (moon) \1
This one searches for the word "moon", then wants to see it "copied" right after. 
Again, the \1 is the "paste".

### Look-ahead and Look-behind

What are they?
Look-aheads and look-behinds allow you to sneak peak at words before or after your main word, without actually grabbing them.

How are these helpful?
Sometimes you want to find a word, but only if it has a buddy word next to it. 
These tools let you set up those conditions.

Look-Ahead: ( Peeking Ahead )
Pattern: rain(?= bow)
What It Does: Checks for "rain" only if "bow" comes right after.

Look-behind: ( Peeking Behind )
Pattern: (?<=sun )rise
What It Does: Finds "rise" but only if "sun" was right before it.

Essentially, look-behind and look-ahead are, tricks to check the text before or after pattern without grabbing it.
The email regex doesnt utilize look-aheads or look-behinds in main example. These are good tools to know, but not always needed.

### Sources

A list of helpful places to learn more about regex.

Links:

- [Regex Crossword](https://regexcrossword.com/)
- [Regular Expressions.info](https://www.regular-expressions.info/email.html)
- [Anchors](https://www.regular-expressions.info/anchors.html)
- [JavaScript RegExp Reference](https://www.w3schools.com/jsref/jsref_obj_regexp.asp)
- [Stack Overflow](https://stackoverflow.com/)
- [Regular expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions?fbclid=IwAR0Ffg_ibaJt_ZFzl2Wjy9ziYNCGlWVNtP-8Ucn4JRRNIrjNKC85a0fbGCI)
- [Regular expression syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet?fbclid=IwAR2g29IIeP0F3gPS8I6mY5dAY-REPY7S4Z6P68MEF1A2W9wkSZoBfwt2_UY)
- [Regex tutorial](https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285)
- [The Complete Guide to Regular Expressions (Regex)](https://coderpad.io/blog/development/the-complete-guide-to-regular-expressions-regex/?fbclid=IwAR2NeB1kgZMRPLRrXmqwD6MrQRf9X5yqPqopjzWY4JXCZOVCAQgVATgSC_8)
- [Regular expression WIKI](https://en.m.wikipedia.org/wiki/Regular_expression?fbclid=IwAR179NbmJKefHovpCJGOpHwkk1PAOrOaemcJpVSUIvnddqRhmUovgA-8EvU)

## Author

Author: Peyton Mastropolo.
If you have any questions, feel free to contact me on my Github ( Link added below )
Github link: https://github.com/pmastropolo