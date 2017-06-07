# Javascript
## Format of Variables Names
// Class: WordCapitalize

var MyClass = ...

// Variables and functions: camelCase

var myVariable = ...

// Constants: UPPERCASE_WITH_UNDERSCODE

const MY_CONST = ...

## Indent
Indent with 2 spaces (not tabulations).

For our projects, you should always assign variables in a new line, not separated by commas:

// Bad

var a = 1,
    b = 2,
    c = 3;

// Good

var a = 1;
var b = 2;
var c = 3;
Use [] to assign a new Array, NO new Array().

Also, use {} to create new objects.

Below are two scenarios for the use of [], one can be on a single line, the other not so much:

// Good on a single line

var stuff = [1, 2, 3];

// Never on a single line

var longerStuff = [
    'some longer stuff',
    'other longer stuff'
];
## Never assign multiple variables on the same line
BAD bad

var a = 1, b = 'foo', c = 'wtf';

## DO NOT align variable names
Bad:

var wut    = true;
var boohoo = false;

## semicolons<
Use them.

Not because the automatic insertion of semicolons (ASI) is black magic, do it for consistency.

## Conditionals and loops
// Bad

if (something) doStuff()

// Good

if (something) {
    doStuff();
}
## Spaces after a keyword and before the bracket
// Bad

if(bad){

}

// Good

if (something) {

}
# Functions
## Functions with names
Always use named functions, even if you are assigning it to another variable or property. This improves the error stacks when debugging is done.

Do not place spaces between the function name and the initial parenthesis, but if between the closing parenthesis and the initial square bracket:

var method = function doSomething(argOne, argTwo) {

}
## Anonymous Functions
You're doing it wrong, read about the named functions above.

## Operators
You should always use === with the only exception of comparisons with null and undefined.
Example:


if (value != null) {

}
## Quotation marks
Always use single quotes: 'no doubles'

The only exception: "Do not escape single quotation marks in strings like this: \ 'Use double quotes."

## Comments
For functions in node, always provide a clear comment with the following format:

/ * Brief explanation of what is done
  * Expects: any parameter accepted
  * Returns: anything returned
  * /
If the comments are really long, use the / * ... * / format. Otherwise, use short comments like:

// This is a short comment and ends with a period.

## Ternary Operatos
Try not to use them.

If a ternary uses several lines, do not use it:
// Bad

var foo = (user.lastLogin > new Date().getTime() - 16000) ? user.lastLogin - 24000 : 'wut';

// Bueno

return user.isLoggedIn ? 'yay' : 'boo';

## Best Practices
If you realize that you are repeating something that can be a constant, use a single constant definition at the beginning of the file.

Define regular expressions as constants at all times.

You should always test for certainty:

// Bad

if (blah !== false) { ...

// Good

if (blah) { ...

If the code is too long, try breaking it in several lines or refactor it. Try to stay within the limit of 80 columns per line, but if you spend a little is not a big problem. When you break a line, indent the subsequent one level (2 spaces)

If the code looks too smart, it probably is, so just keep it simple.
