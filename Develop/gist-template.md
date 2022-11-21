# Regex-Tutorial
As a developer, I want to create a tutorial that explains how a specific regular expression, or regex, functions by breaking down each part of the expression and describing what it does.

## Summary
A Regex or regular expression is a sequence of characters that define a search pattern. Usually such patterns are used by string-searching algorithms for "find" or "find and replace" operations on strings. It also looks for input validations. It is a technique commonly developed in theoretical computer science.

We will look a a string of code using regex, this code looks for a match HTML tag.
```
/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/
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
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors
* `^abc$`	-^start / $end of the string
    * `^` Matches the beginning of the string, or the beginning of a line if the multiline flag (m) is enabled.This matches a position, not a character.
    * `$` Matches the end of the string, or the end of a line if the multiline flag (m) is enabled. This matches a position, not a character.

* `\b\B`	-word, not-word boundary
    * `\b` Matches a word boundary position between a word character and non-word character or position (start / end of string). See the word character class (w) for more info.
    * `\B` Matches any position that is not a word boundary. This matches a position, not a character.
    * See Boundaries for more detailed Information

### Quantifiers
* `a*a+a?`	-0 or more, 1 or more, 0 or 1
    * "+" Matches 1 or more of the preceding token.
    * "*" Matches 0 or more of the preceding token.
    * "?" Matches 0 or 1 of the preceding token, effectively making it optional.
    * "?" Makes the preceding quantifier lazy, causing it to match as few characters as possible. By default, quantifiers are greedy, and will match as many characters as possible.

* `a{5}a{2,}`	 -Looks for exactly five, two or more
* `{2,6}`  	    -forces the input of characters between two & six characters long.
* `a+?a{2,}?`	 -match as few as possible
* `ab|cd`	    -match ab or cd

### OR Operator
* `|`
    * This operator acts like a Boolean OR. It causes a match of the expression before or after the `|` and can be utilized inside a group or on a whole expression. In terms of order, it causes the search-string to look for a match of either what precedes or follows after the `|`. In the example: `<abc>|<cba>` it is looking for either `<abc>` or `<cba>`.

### Character Classes

In order to search for match characters between a specific range of character, we create what is called "character classes".

Some example types:

* `\w` This will match any word character (alphanumeric and underscored) such as `[a-z0-9_]`, but will only match lowercase character without accent marks.

* `\W` This matches any character that is not a word character (alphanumeric and underscored) such as `[A-Za-z0-9_]`

* `\d` sets the search to match any digitized character such as `0-9`

* \D` sets the search for non-digitized characters

* `\p` sets the match for a character in the specific unicode category

* `[A-Z]` utilizing the hyphen between the two characters creates a range for the search criteria

* `'` is a wildcard and will accept any input

### Character Classes
Character classes match a character from a specific set. There are a number of predefined character classes and you can also define your own sets.

* `[ABC]` Characters inside brakets will match any character in the set.
* `[^ABC]` Adding a caret will match any character that is not in the set.
* `[A-Z]` Add a dash between two characters will select a Range.
* `.` Will Match any characters expect linebreaks. Its like a wildcard and will accpet any input.
* `[\s\S]` A character set that can be used to match any character, including line breaks, without the dotall flag. An alternative is [^] carrot in brackets, but it is not supported in all browsers.
* `\w` Matches any word character (alphanumeric & underscore). Only matches low-ascii characters (no accented or non-roman characters).
* `\W` Matches any character that is not a word character (alphanumeric & underscore).
* `\d` Matches any digit character (0-9)
* `\p` Matches a character in the specified unicode category.

### Flags
To change how an expression is interpreted, expression flags are used following the initial closing forward slash expression.

* `i` ignores case

* `g` is a modifier to perform a global match which finds all matches instead of stopping after the first match. For case-sensitive matches, combine `g` with the `i` modifier.

* `m` is a multiline flag enabled to match the start and end of a line, rather than the start and end of a whole string. The anchors used at the beginning and end should reflect what we've learned previously: `^` and `$`.

* `s` is a global search for whitespace characters within a string

### Grouping and Capturing
* `(abc){3}` if we desired to group a selective pattern, we can introduce them between parentheses and include a numeric counter besides it. This example would search for the match of `abcabcabc` because the first group was denoted as `(abc)` and we included the need for it to repeat three times as `{3}`.

For non-capturing parentheses groups, the regex would look similarly `(?:abc){3}` or `(?:ABC`.

### Bracket Expressions
A regular expression surrounded by square brackets is considered a bracket expression meant to match a single character or collating element. When the first character is a circumflex `^` then the bracket expression is complemented. An example is `[a-z]` as a bracket expression. 

### Greedy and Lazy Match
Earlier, greedy and lazy matches were briefly remarked in [Quantifiers](#quantifiers). 

A greedy quantifier tells the search algorithm to match as many instances of the pattern presented as possible. It is the longest possible string match.

A lazy quantifier is considered the shortest match and tells the search algorithm to match as few of the patterns searches as possible. You can make a regular quantifier lazy by adding `?` to the end of it.

### Boundaries
The `\b` is an anchor like the caret and the dollar sign. It matches at a position that is called a “word boundary”. This match is zero-length.

Characters that are matched by the short-hand character class `\w` are the characters that are treated as word characters by word boundaries.

Since digits are considered to be word characters, `\b4\b` can be used to match a 4 that is not part of a larger number. So saying `\b` matches before and after an alphanumeric sequence is more exact than saying “before and after a word”.

`\B` is the negated version of `\b`. `\B` matches at every position where `\b` does not. Effectively, `\B` matches at any position between two word characters as well as at any position between two non-word characters.

There are more boundries with the Regex Engine. Some examples include Tcl, GNU, and POSIX.

### Back-references
Backreferences match the same text as previously matched by a capturing group. Suppose you want to match a pair of opening and closing HTML tags, and the text in between. By putting the opening tag into a backreference, we can reuse the name of the tag for the closing tag.

For Example: `<([A-Z][0-9]*)\b[^>]*>.*?</\1>` This regex contains only one pair of parentheses, which capture the string matched by `[A-Z][0-9]*`. This is the opening HTML tag. The backreference `\1` references the first capturing group. `\1` matches the exact same text that was matched by the first capturing group. The `/` before it is a literal character. It is simply the forward slash in the closing HTML tag that we are trying to match.

### Look-ahead and Look-behind
Also known as "lookaround", the Look-Ahead and Look-Behind are zero-length assertions. The main difference with it is that they actually match characters and gives up the match, returning only the result: match or no match. They are called "assertions" since they do not consume the characters in the string, but assert whether a match is possible or not.

A lookaround allows the creation of regular expression that are otherwise impossible to create without them or that would become very longwinded without the usage of them.

## Author
Jie Zou: [GitHub](https://github.com/Zoujiejie), [LinkedIn](https://www.linkedin.com/in/jie-zou-2779ab161/)
