# Regex Tutorial

Breaking down and understanding how to match an HTML tag using Regex.

## Summary

Before we begin, What is a regex? A regex aka "<b>REG</b>ular <b>EX</b>pression," is a chain of characters used to define a specfic search pattern.

In this tutorial, we will break down the following regex used to find and match an HTML tag:
```md
Regex
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/

Matching String
<p id="regexTag">Hello World</p>
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)

## Regex Components

### Anchors
In our regex, we have two anchors: <kbd>^</kbd> and <kbd>$</kbd> . These two anchors are representing the <i>start of a string</i> <kbd>^</kbd> and the <i>end of a string</i> <kbd>$</kbd>\.

### Quantifiers
In our regex, we have two "Greedy" quanitifiers, <kbd>*</kbd> and <kbd>+</kbd> being used.

([See Greedy and Lazy Match](#greedy-and-lazy-match))

### OR Operator
The OR Operator is also known as an 'Alternate' and uses the OR syntax <kbd>|</kbd>. 

Example:
```md
match either a|b
```
Case sensitive*

### Character Classes
In our regex, we have two Bracket Expressions ([See Bracket Expressions](#bracket-expressions)) AKA Character Classes, or simply Classes. Classes are declared with <kbd>[ brackets ]</kbd>.

Class 1
```md
[a-z]
```

Class 2
```md
[^<]
```

### Flags
In our regex we have no flags declared, however - a flag, also known as a modifier, can be put on the end of a regex to give a regex an even more specific search pattern. Some of the most basic flags are:
```md
> Global: g
> Multiline: m
> Case insensitive: i
> Sticky - searches in strings only from the index of the last match: y
> Enable unicode support: U
```
An example in our regex would be as followed:
```md
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/g
```
Notice the flag <kbd>g</kbd> is placed AFTER the last <kbd>/</kbd>.

### Grouping and Capturing
In our regex, we have 4 groupings:

CapGroup 1
```md
([a-z]+)
```
CapGroup 2
```md
([^<]+)*
```
Non-CapGroup 1
```md
(?:>(.*)<\/\1>|\s+\/>)
```
CapGroup 3
```md
(.*) - this group is inside of Non-CapGroup 1
```
Nested inside CapGroup 1 and 2 are "Bracket Expressions" ([See Bracket Expressions](#bracket-expressions)).
Nested inside Non-CapGroup 1, we have two(2) alternative arguments seperated by the OR (Alternate) syntax <kbd>|</kbd>\. [See OR Operator](#or-operator)

In our CapGroup 1 and 2, we are <i>Capturing</i> everything enclosed inside the <kbd>( paraentheses )</kbd>.

Undstanding CapGroup 1: <code>([a-z]+)</code>... We are capturing everything inside the <kbd>( )</kbd>. If we did not have the <kbd>+</kbd> quantifier, we would only capture one(1) character. Since we did declare the (Greedy) <kbd>+</kbd> quantifier, we will capture all characters in a chain, and stopping at whitespace or symbols. This Group finds and matches the following:
```md
<p>
```

Understanding CapGroup 2: <code>([^<]+)*</code>... We are capturing everything inside <kbd>( )</kbd>. Inside our bracket expression we are trying to find and match any character, whitespace and special characters in a chain. using <kbd^</kbd> will match a non listed character once. But, because we declared a <kbd>+</kbd> quantifier, we now will capture and match all characters including whitespace and special characters. This group finds and matches the following:
```md
 id="regexTag" , including whitespace. (Notice: There is whitespace behind the "i". It is found and matched by this group.
```
&#9889; We also declared the <kbd>*</kbd> character. This will allow and match the previous token(group) - <code>([^<])</code>, from zero(0) to unlimited time, as many times as needed. [See Quantifiers](#quantifiers)

In our Non-CapGroup - <code>(?:>(.*)<\/\1>|\s+\/>)</code> we have two(2) alternatives declared by the OR <kbd>|</kbd> syntax. We are <i>Matching</i> everthing enclosed inside the <kbd>( )</kbd> by using the <kbd>?:</kbd> at the beginning of the syntax. We then have our 3rd group expression (See Below). Then, we are declaring a literal for the <kbd>/</kbd> character using <kbd> \ </kbd>. [See Text and Oddies](#texts-and-oddies).
  
First Alternative:
```md
\1 matches the same text as the most recent matched by the 1st group.
```
OR <kbd>|</kbd>
  
Second Alternative:
```md
\s matches any whitespace.
```
> This allows our closing HTML tag to match the opening HTML tag...
 
In our CapGroup 3, we are matching any character, including whitespace - <i>except for line terminators</i>

&#9889; Line Terminators are: \n, \r, \u2028, \u2029

### Bracket Expressions
Bracket Expressions refer to a matching or non-matching list characters. These list are case sensitive - a is not the same as A, etc...
For example, our regex has 2 bracket expressions:

Expression 1
```md
[a-z]+
```
Expression 1 will match a list of characters from a through z until hits whitespace or any symbols.
For example, <code>regex is strange!</code> will match <code>regex</code>

Expression 2
```md
[^<]+
```
Using the <kbd>^</kbd> syntax inside a bracket expression will declare a non-matching list. This regex expression also uses the <kbd><</kbd> symnbol which will match a text character presented to it. Expression 2 will match all charatcers including whitespace and symbols.

### Greedy and Lazy Match
The <kbd>+</kbd> quantifier will match a token from <i>one(1) to unlimited times</i>. In our regex, the tokens are the bracket expression <code>[a-z]</code> and <code>[^<]</code>), giving back as needed. This is known as a "Greedy" match.

Meanwhile, the <kbd>*</kbd> quantifer with match a token from <i>zero(0) to unlimited times</i>, giving back as needed. This is known as a "Greedy" match.

Not shown, however a "Lazy" match will match as few characters as possible. You can do this by providing a <kbd>?</kbd> as a quantifier.
  
### Texts and Oddies
<kbd><</kbd>, <kbd>></kbd>, <kbd>/</kbd> are just text characters to match.
  
When a <kbd> \ </kbd> is declared, we are making any character a literal.

## Author

I am a graduated engineering student and i love coding...
  
You can check out my github account here!
> https://github.com/cumauu73