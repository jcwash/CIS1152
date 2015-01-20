# Lecture 2A

## Conditional Statements
### The if Statement

In most C-style languages, there are two basic conditional statements, the if statement and the switch statement (also sometimes called the case statement). PHP is no exception. We are going to start with the if statement. It is the easier of the two.

The if statement is a simple concept. If something is true, then perform the statement block associated with it; otherwise skip the associated code. To use conditionals, you need to be evaluating an expression that evaluates to true or false. We have discussed conditional operators elsewhere, but we can also test for non-zero, non-null, non-empty values in variables, and many system defined functions return true or false depending on their successful execution.

The if statement takes the form of:

```php
if (conditional expression) {
    statement block;
}
```

If some conditional expression evaluates to true then PHP performs the associated statement block. For instance, the following statement will echo out a warning that the value of a variable is not an integer. It will only generate this message if the expression !is_int($x) evaluates to true, which is to say, if it is not a number.

```php
if (!is_int($x)) {
    echo ($x . ' is not an integer!');
}
```

If you just want to execute a single statement within an if statement, you do not technically need the curly brackets, but they are a good habit to get into so you don't forget them.

### The else Statement

The if statement executes a block of code if something is true.

What happens if you want to execute one block of code if something is true and another if it is false? In this case, PHP has something called the else statement.

The else statement can only follow an if statement and is used to mark off a statement block to execute if the conditional expression being tested evaluates to false. It does not take its own test condition expression because it executes in response to the if statement immediately preceding it returning false.

```php
if (!is_int($x)) {
    echo ($x . ' is not an integer!');
} else {
    echo $x . ' is a number we can work with!');
}
```

Don't forget the curly brackets around both expression blocks. Thinking that the else is part of the if statement (which technically it is) makes it easy to forget to close the if statement block before the else statement block.

### The elseif Statements

What happens if you want to test for more than simply whether a given expression equates to true or false, but want to test for and execute code based on a variety of possible conditions? Which is to say, what happens if there are three or more conditions.

PHP has an elseif statement. This allows us to test for another conditions if the first one wasn't true. The program will test each condition in sequence until:

- It finds one that is true. In which case it executes the code for that condition.
- It reaches an else statement. In which case it executes the code in the else statement.
- It reaches the end of the if … elseif … else structure. In this case it moves to the next statement after the conditional structure.

The elseif sturcture looks like this:

```php
if (is_int($x)) {
    echo ($x . ' is an integer');
} elseif (is_float($x)) {
    echo ($x . ' is a floating point number');
} elseif (is_string($x)) {
    echo ($x . ' is a string');
} elseif (is_bool($x)) {
    echo ($x . ' is a boolean');
} else {
    echo ($x . ' is not a primitive data type');
}
```

### The switch Statement

Although you can test for multiple conditions with a series of if statements, the if statement really does only test the truth of a single conditional expression at a time. It is a two state expression, either the statement block executes or it doesn't.

If you want to check a single variable for multiple values, you can do so with a series of if statements, but this is not always the best approach. PHP also provides a conditional statement for testing multiple values for a single variable or expression. This is the switch statement.

The switch statement, in its structure, is similar to the if statement. It takes an expression to be evaluated and a statement block.

The switch statement can only evaluate a single expression, but it can compare that single expression to a series of possible values. The expression to be evaluated is most likely not a conditional, since a conditional only has two possible states -- something best handled by an if … else statement. Rather it is usually some expression that can have a series of values, such as a variable that can have a number between 0 and 9, or a form field that can contain one of the fifty two-character abbreviations for the U.S. state names.

```php
switch (expression) {
    statements;
}
```

Although the shell of the statement is the same, the body of the statement block is significantly more complex and requires additional keywords to make the statement work. A full switch statement may look like the following example.

```php
switch ($myState) {
case "NY":
    echo "You're from New York";
    break;
case "VT":
    echo "You're from Vermont";
    break;
case "MA":
    echo "You're from Massachussetts";
    break;
default:
    echo "You're not from around here";
    break;
}
```

Let us look at the various elements.

#### The case Statement
A label is an identifier in the code used to assign a name to that specific location in the code. The case keyword is a label; it marks a point in the code to do something. Specifically it marks the point in the code to begin executing statements if the value of the expression being evaluated by the switch statement is equal to the value immediately following the case keyword or if the expression following the case keyword evaluates to true. The colon marks the end of the label. The entire label should be on one line.

In PHP, the case statement takes an expression, which must equate to true for the following code to be run. If you are doing simple equality then you can just provide the value you are checking for and it assumes that the expression is testing the switch expression against the value in question for equality. However, by allowing expressions, you can also test for other conditions, such as greater than and less than relationships. When using expressions, the expression you are testing against must be repeated in the case statement.

```php
switch ($someNumber) {
    case 0:
        echo "Zero is not a valid value.";
        break;

    case $someNumber \< 0:
        echo "I can't use negative numbers.";
        break;

    default:
        echo "Ready to compute.";
        break;
}
```

If an expression successfully evaluates to the values specified in more than one case statement, only the first one encountered will be executed. Once a match is made, PHP stops looking for more matches.

In the following case, the second case will never be executed, because anything greater than 1000 is also greater than 100.

```php
switch ($someNumber) {
    case $someNumber \> 100:
        echo "The number is greater than 100.";
        break;
    case $someNumber \> 1000:
        echo "The number is greater than 1000.";
        break;
}
```

The way around this is just to make sure that the conditions are specified in the correct order for what you want them to do.

```php
switch ($someNumber) {
    case $someNumber \> 1000:
        echo "The number is greater than 1000.";
        break;
    case $someNumber \> 100:
        echo "The number is greater than 100.";
        break;
}
```

#### The default Condition
The default keyword is a catchall case that marks the point to begin execution if none of the conditions being tested for are met. It is like the last else statement in a long string of elseif's.

Like the last else, it should always appear at the end of the switch statement, since it will always be executed if no previous match has been made, and since PHP stops looking when it finds a match. Default is always a match if it is reached. You should only use it if you have code that is to be run if none of the conditions are met. For instance, error code to report that the expression did not evaluate to an expected value.

#### The break Statement
The break keyword is a statement that says that we are done performing statements within this statement block and that we should exit immediately to the end of the statement block. If you forget the break statement, then the code will fall through, which is to say that the code will start executing at the label that matches the value of the expression being evaluated, and then will proceed to process all code until either the end of the switch statement or until it find a break statement, which ever comes first. If done intentionally, this can be useful. If done by mistake it can be a real problem.

Here is a good use of omitting break statements. It allows use to perform the same black of code for multiple possible values of the expression being evaluated.

```php
switch ($xyz) {
    // each of these three cases will process the same statements
    case $xyz \< 0:
    case 0:
    case 10:
        echo ($xyz . ' is not a value I can work with!');
        break;
    default:
        echo ($xyz . ' is ready for processing!');
        $abc = someFunc($xyz);
        break;
}
```

Here is a bad example of omitting break statements. The code will fall through and create a bit of a mess.

```php
// A poorly formed switch statement

switch ($xyz) {
    case is_int($xyz) == false:
        echo ($xyz . ' is not an integer!');
    case $xyz \<= 0:
        echo ($xyz . ' is too low!');
    case $xyz \>= 10:
        echo ($xyz .+ ' is too high!');
    default:
        echo ($ xyz . ' is within acceptable limits!');
        $abc = someFunc($xyz);
        break;
}
```

If we assume for right now that $xyz is not an integer:

- The code will report that $xyz is not an integer.
- Then report that it is too low a number.
- Then report it is too high.
- Then it report that it is an acceptable value.
- Then it will submit it to our function, which we can surmise from the code, was expecting a numeric value between 1 and 9,not something else. This, needless to say, would most probably generate an error.

Unless your goal is to confuse the user, what you would have is what is called a big mess.

The break statement can also be used in an odd way in PHP that can cause errors if you are not aware of it. If the break statement is the only statement following a given case statement, the code will skip to the default statement block instead of the end of the switch statement.

This may seem a little odd for experienced programmers because it raises the question, why include a separate case statement for case statement for something that should fall into the default. The primary reason is that it allows you to exclude certain values that might otherwise meet a later condition. For instance, if we go back to our previous example and wanted to code to run the default statements for a number between zero and nine or for any number divisible by 10, we could code:

```php
switch ($xyz) {
    case is_int($xyz) == false:
        echo ($xyz . ' is not an integer!');
        break;
    case $xyz \<= 0:
        echo ($xyz . ' is too low!');
        break; // the following statement will skip to the default
    case $xyz % 10 == 0:
        break;
    case $xyz \>= 10:
        echo ($xyz .+ ' is too high!');
        break;
    default:
        echo ($ xyz . ' is within acceptable limits!');
        $abc = someFunc($xyz);
        break;
}
```

### Other Formats
PHP likes to cover its bases, so it provides alternate methods for
coding if statements and switch statements.

#### Alternate if
There are two alternate ways to code an if statement, one is a ternary operator, and one is an alternate syntax.

The ternary operator takes the form of:

```php
(condition) ? value_if_true : value_if_false;

$hours = ($hours \< 13) ? $hours : $hours -= 12;
```

Since the ternary operator is, in fact, an operator, it returns a value, which is the value of one of the expressions. If the condition evaluates to true, then the first value is returned (value\_if\_true), otherwise the second value is returned (value\_if\_false). This means that the expressions for the true and false values need to be things that evaluate to values, not full blown statements, just simple expressions.

## Iteration
Some statements in PHP are known as iterative statements. These
statements have control structures that delimit them and which determine
how many times (zero or more) the delimited code is executed, based on
some condition.

We will look at three structures here:

-   the while statement and its variants

-   the do ... while statement

-   the for statement

We will also look at some more advanced ways of working with iteration
by being able to more freely move between nested iterative statements.

### The while Statement

The while statement is the most basic of iterative control structures.
It is also known as a prefix look. It repeatedly runs a block of code
until some condition is no longer true. If the condition is not true to
begin with, then the code never runs. It takes the form of:

while (expression) {

statements;

}

For example, if we wanted to add together the first ten values from an
array:

$x = 0;

while ($x \< 10) {

$a = $a + $b[$x];

$x++;

}

In the above code, we initialize a variable to zero (0) before beginning
the loop. The while statement then evaluates the conditional expression.
This expression must be inside parentheses. In this case, zero is less
than 10, so the statement executes.

In the body of a while statement there must be some code that changes
the value of the condition. Otherwise the loop will never terminate.

The last line in the statement block increments the variable we are
testing in our conditional expression. In the body of a while statement
there must be some code that changes the value of the condition.
Otherwise the loop will never terminate. In the following code, the
conditional expression will never become false, so the code will run
forever (or until it crashes).

// bad code -- an infinite loop

$x = 0;

$z = 0;

while ($x \< 10) {

$a = $a + $b[$z];

$z++;

}

This state of endless execution is known as an infinite loop. An
infinite loop is an iterative code element that has no valid termination
condition, meaning it will never stop looping. A bit of trivia, it is
also the street on which Apple’s headquarters is located ([Apple
Computers Corporate Address](http://www.apple.com/contact/)). Anyone
with any programming experience is all too familiar with them. Their
causes are many, and they are far too easy to create.

Like the if and switch statements from our previous lecture, while has
an alternative label based syntax.

while (expression):

statements;

endwhile;

### The do while Statement

A while statement will never execute if its conditional expression never
evaluates to true. What happens if you want the code to always run at
least once, regardless of the value of its conditional expression? The
answer is use a do while statement. A do while statement is also known
as a post fix loop.

A do while statement is like a while statement in reverse. First it runs
the block of code, and then it evaluates the conditional expression. If
the conditional expression is true, then it loops back to the beginning
of the statement and starts again.

It takes the form of:

do {

statements;

} while (expression);

Note that since the curly brackets do not end the entire statement, we
need a semi-colon at the end.

An example:

$x = 0;

do {

$a =$ a + $b[$x];

$x++;

} while ($x \< 10);

This code will have the same effect as the equivalent while loop above.
One that would work differently might be as follows:

// will never run since the initial state of $x is $x != 10

$x = 0;

while ($x == 10) {

$a = $a + $b[$x];

$x++;

}

// will run once even though the initial state of $x is $x != 10

$x = 0;

do {

$a = $a + $b[$x];

$x++;

} while ($x == 10);

A more practical use for this loop might be to check whether something
has a value. For instance, you could walk an array as long as you keep
finding values.

$x = 0;

do {

if ($aName[$x]) {

$bName[$x] = someProc($aName[$x]);

}

$x++;

} while (isset($aName[$x]));

In the preceding example, we take advantage of the fact that
non-existent value return false. This example assumes all the array
elements are contiguous, since it will stop executing with the first
empty array element it finds.

The do while has no alternative syntax, partly since anything you can do
with a do while statement you can also do with a while statement. The do
while is just easier to read in certain circumstances. It is also partly
because the while, in occurring at the end, would be indistinguishable
from a nested while loop if the curly brackets were omitted.

### The for Statement

The for statement allows for incremental processing based on some
incremental variable. The for statement is also known as an iterative
loop. Unlike the while statement, the variable is incremented within the
conditional expression itself. This means that you do not have to have
code in the body of the statement to set the termination condition. This
does not mean you that you cannot set the termination condition in the
body, merely that you don't have to.

It takes the form of:

for (init; condition; increment) {

statements;

}

The three values that go inside the for statement conditional expression
are:

-   init -\> The initial state of the variable to be tested. Normally
    done as an assignment, although the assigned value can be from any
    source, literal or variable.

-   Condition -\> The condition to be tested for. The statement keeps
    processing as long as it remains true.

-   Increment -\> The increment by which the variable being tested
    changes.

For example:

for ($x = 0; $x \< 10; $x++;) {

$a = $a + $b[$x];

}

For those who want to do things the hard way, you can also specify
multiple conditions by putting them in a comma separated list within the
semi-colon separated list.

for ($x=0,$y=0; $x\<10,$y\<20; $x++,incrF($y);) {

$a = $a + $b[$x];

}

This iterative structure also has an alternative syntax.

for (init; condition; increment):

statements;

endfor;

For and while are not one hundred percent interchangeable, so think
about which one you want to use before coding.

The for statement assumes some sort of incrementation, such as counting
through a set of something. It is designed for stepping through things.

Although any basic discussion of iteration tends to use incremental
examples for both while and for statements, the while statement is
better suited for testing some flag or condition. A flag, in programming
terms, is a variable, usually boolean, that refers to the current state
of something the in the program. Our example above of using a while
statement to walk an array is an example where we are testing the
contents of the elements of an array, not our position in it.

### Termination Statements

Sometimes you want to break out of a control statement early, perhaps
because of an error or some other condition that the conditional
expression itself is not testing for. We have seen an example of this
already with the break statement used in a switch statement-coding
block.

Here we will look at various ways to prematurely terminate loops and
conditionals by setting multiple exit points.

#### The break Statement

Break breaks you out of the conditional statement and moves on to the
first statement outside of the conditional statement. When using break
to get out of a condition, be aware that it ignores if statements. This
is so you can use an if statement to test whether you need to terminate
the current conditional.

For instance, we could use it to modify a previous do while statement.
In the following example, the code will now terminate if the value to be
processed is not an integer.

$x = 0;

$rVal = "";

do {

if (isset($aName[$x])) {

if (is_int($aName[$x])) {

$rVal = "Bad Value";

break;

}

$bName[$x] = someProc($aName[$x]);

}

$x++;

} while (isset($aName[$x]));

#### The continue Statement

If you are using an iterative statement and don't want to terminate it,
just skip the current instance or iteration, you can use the continue
statement. Continue says that the current iteration is done and the next
one should be started. This is useful if the statement block has
multiple possible exit points.

$i = 0;\
while ($i++ \< 5) {\
    echo "Outer\<br /\>\\n";\
    while (1) {\
        echo "&nbsp;&nbsp;Middle\<br /\>\\n";\
        while (1) {\
            echo "&nbsp;&nbsp;Inner\<br /\>\\n";\
            continue 3;\
        }\
        echo "This never gets output.\<br /\>\\n";\
    }\
    echo "Neither does this.\<br /\>\\n";\
}

#### Cautionary Note

It is always best to build your code in such a way that the logic of
your algorithm completes every possible outcome. While break and
continue can be useful they are considered sloppy coding practice. The
main reason for this is it obfuscates your code and makes it hard to
follow. Break and continue statements should be avoided if at all
possible. The only exception to this switch statement; where it is a
construct of the control structure.

## Functions


A function is a statement block that has been assigned a name. That name
allows it to be called or referred to, meaning the function can be
invoked by name to perform some task, or function. This means that you
can create a piece of code that will not run until specifically called
for or invoked by another piece of code.

Being able to defer the execution of code until it is called for is a
very powerful tool. It allows us to step out of linear, batch processing
mode and instead operate in an event driven environment.

For students coming directly from Programing and Logic I, think of a
function as a classless method.

Defining Functions
------------------

In PHP a function is defined as follows:

function functionName(parameter) {

statements;

return;

}

-   The definition starts with the keyword function.

-   This is followed by the name of the function.

-   After that comes a set of parentheses containing the parameters, or
    input values, the function is expecting to receive. Each parameter
    must be a variable name. These variables are created by declaring
    them as parameters and are local to the function. Sometimes you will
    hear parameters called arguments. Technically an argument is what is
    sent and a parameter is what the function is expecting to receive.
    Most textbooks authors pick one or the other term and just stick
    with it, so you can consider them to be interchangeable words.

-   After this comes the curly braces that delimit the statement block
    that makes up the body of the function.

-   The last statement in the statement block should be a return
    statement, which returns control back to whatever called the
    function. The keyword return can stand-alone or it can be followed
    (with no intervening line break) by a value to be returned. If no
    value is specified, then the function returns null.

function testVal($x) {

if (!(is_int($x))) {

echo "$x is not a number!";

}

return;

}

function strangeEquation(x, y, q) {

var z = x \* y;

var p = q - 7;

return (z \* x % (y + 1)) / p;

}

When trying to figure out what to name your functions, you only need to
remember a few basic rules.

-   PHP function names are not case sensitive. Therefore, fname(),
    Fname(), and FNAME() all refer to the same function.

-   The function name can only contain letters from the ASCII character
    set, digits, and the underscore.

-   The function name cannot begin with a digit.

-   You cannot give a function the same name as another function or
    reserved keyword. PHP does not support function overloading.

Invoking Functions
------------------

You invoke, or call, a function by name. The name needs to be followed
by a set of parentheses that contain zero or more values to be passed to
the function, called the arguments for the function call. The number of
values being passed should be equal to the number of parameters of the
function. The values are assigned to the parameters in the order in
which they appear defined in the function's parameter list.

Invoking a function:

$x = 'bob';

testVal($x);

$x = 1;

$y = 2;

$q = 3;

strangeEquation($x, $y, $q);

If you want to pass values of a certain type, you need to test for this
yourself since PHP, being a loosely typed language, does not check.

If you pass too many arguments, then the additional values do not get
assigned to named parameters. They can still be accessed within the
function, just not as named variables from the parameter list.

If you pass too few arguments, then the remaining parameters will be set
to null. PHP will generate an error message about this, but will try to
run the function anyway.

If you don't want to pass certain arguments, you cannot use the empty
comma notation as you can in some languages. Instead you just need to
put null values in those locations.

$x = fName(,,$c); // incorrect

$x = fName(null,null,$c); // correct

### Passing by Reference

PHP always passes by value, including objects and arrays. There are two
primary models for passing data back and forth in a program. One is
passing by value and the other is passing by reference. Passing by value
means that when you pass the variable by sending it as an argument to a
function, or assigning it to another variable using an assignment
operator, a copy of the value of the variable is made and that is what
is passed to the receiving function or variable.

It works like this: If I set $a equal to 7, and then say $b = $a, I
will then have two variables each storing the value if 7. If I change
either one, it won't affect the other one. It is like a photocopy. After
I have made the copies, writing something on one copy won't affect the
other copies.

Passing by reference is a little more complicated and normally only
occurs in object oriented environments. To understand it, it first helps
to understand that variables are actually just pointers pointing to
values stored in memory. Passing by value works by creating a new
pointer pointing to a new location in memory with a copy of the stuff
from the old location copied over to the new location. Passing by
reference created a new pointer but points it to the exact same
location. It is not actually passing the value anywhere; it is just
creating new variables pointing to the exact same thing. Another way of
saying it is that it creates an alias for the current variable instead
of making a copy.

Passing by reference is not something that is needed very often. So, I
will not spend time covering it here. If you find yourself in need of
this particular skill, please refer the PHP Manual section on this topic
([References
Explained](http://php.net/manual/en/language.references.php)).