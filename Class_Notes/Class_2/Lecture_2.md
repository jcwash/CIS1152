# Lecture 2

## PHP Basics
### Embedding PHP

PHP is an embedded language. What is an embedded language you ask? An embedded language is a coding language that is embedded in the data file, which it is acting upon. Unlike some embedded scripting languages (JavaScript for instance), PHP can also be run as a script external to the data it is acting on, and can in fact pull data from multiple sources. However, it is technically a part of the document it produces.

You invoke PHP by making a call to an HTTP server for a document that ends in a .php suffix. The server, seeing the suffix, assumes that there is PHP code embedded in that document that needs to be processed and passes it to a PHP parser for processing before returning the document to the requesting client. (If there is no PHP code, nothing happens, and the document gets sent on as is.) Thus, PHP can modify, overwrite, or even replace the document, depending on circumstance.

As a for instance, I could have a file called myfile.php that would be a script that evaluates what type of browser the client is using and uses that information to substitute a document appropriate to that browser for itself. This would allow me to have one address for the page, even though there may be many different pages to address issues of browser incompatibilities.
On of the most common uses of PHP is to generate dynamic content that is adaptive. It can change the content on a page to suit different browsers. Another common use is assembling data from diverse data sources into a single document for return to the user.

### The XML Processing Directive

![Simplified History of Markup Language](http://csharpcomputing.com/XMLTutorial/xmlevolution.jpg)

For those who aren't familiar with XML, here is the quick overview. SGML, or the Standard Generalized Markup Language, is the original markup language. SGML was created to overcome electronic publish challenges. However, it is very complex and quite strict. It is the forerunner of the family of markup languages that includes HTML and XML and which are used for marking up online content for display.

HTML was derived from SGML to function as a markup language specifically for Web documents. HTML was created to fill the need for a simple markup language to create a webpage. It overcame SGMLs complexity by removing a substantial amount of its flexibility. This simplicity was seen as a disadvantage and so a new language was needed. One that maintained a level of flexibility like SGML but with the ease of use of HTML

The compromise was a new Web language called XML. It was derived from SGML. XML is stricter than HTML but infinitely more flexible. The relationship between the two is close enough that an HTML document, for our purposes, can be treated as a poorly written XML document.

The way in which you normally embed PHP in a document is through what is commonly called a PHP statement, but is actually an XML directive. PHP is designed to be compatible with many standards and commonly used scripting approaches, making it easier to code. Here we are going to code to standards. After we look at the standards-defined method, we will look at the other methods.

An XML processing directive is a command embedded in an XML document for some application to process. All XML processing directives take the form of:

```xml
<? application_name information for application ?>
```

Notice that the statement opens and closes with nested brackets and question marks, and that the name of the application being referenced must come right after the first question mark, with no space before it. The information for the application can be a short statement, or, in the case of PHP, can go on for pages and pages.

The PHP statement normally uses this form of inclusion in HTML documents. It looks like this:

```php
<?php some php statements ?>
```

Line breaks are allowed within the XML processing directive, so the following is also legal.

```php
<?php
 some php statements
and some more statements ?>
```

Since PHP is processed by the server, it can literally go anywhere in an HMTL document in question. The code is processed before the web browser sees the code, so the web browser never sees the PHP. Since you can put it anywhere, PHP can be used to write content, or tag attributes, or even tags. Any of the following might be valid PHP / HTML code combinations.

```php
<p><?php echo "Hello World!"; ?></p>
<?php echo "<h2>" . $item1 . "</h2>"; ?>
<table width="<?php echo $twidth; ?>">
<img src="linkimag.gif" height="10" width="100"
<?php if (!$strict) { echo border='0'; } ?> \>
```

### Introduction To Output
#### Echo and Print
Perhaps the most common use of PHP is to generate content, and the most common means of doing so is the echo and print commands, which writes information back to the document to be sent to the client.

```php
<?php echo "Rasputin" ?>
//or
<?php print "Rasputin" ?>
```

Either command can be used. For our purposes from here on out, I will use echo. I use echo because I am lazy and it is one letter shorter. We will explore output in great depth later on in the course.

### PHP Syntax
PHP is a C-style language. This means that much of its syntax is similar to C. If you are familiar with most any C-style language (C, C++, Java, JavaScript) then PHP should look very familiar. It does, however, have a few little twists and turns you need to know about.

#### The Semi-colon
The first rule is that every statement must end in a semi-colon `;`. The semi-colon is the programmatic equivalent of the period at the end of the sentence. There is only one exception to this rule.  If a statement ends in a curly bracket, then there is no semi-colon after the curly bracket.

```php
<?php
  if ($sometest) {
    echo "it seems that the";  // required
    echo " test is positive";  // required
  }// forbidden
  else {
    echo "it seems that the";  // required
    echo " test is negative";  // required
  }// forbidden
  echo " -- so now you know";  // required
  ?>
```

#### Case Sensitivity
In PHP, only user-defined variables are case sensitive. If you assume everything is case sensitive it makes life easier though. Convention is that predefined function and method names are written in lower case while predefined variable names are written in upper case. User defined variable names are traditionally written in lower case or C-style camelCase (multiWordVar) to differentiate them from the system variables.

#### Whitespace
White space is normally ignored in PHP. This means you can space the code out and put line breaks in as you see fit to make the code more readable.

White space can affect coding in certain circumstances. Normally, it should be a common sense issue in determining where white space is important. For instance, the following code snippet will yield an output of 2.5 -- 25 because the period is the string concatenation operator, but if it is between two numbers with no intervening space, it is a decimal point, just as you would expect it to be.

```php
<?php
  $xyz = 2.5;
  $abc = 2 . 5;
  echo $xyz;
  echo " -- ";
  echo $abc;
?>
```

### Comments
Comments are an important part of coding. They allow you to be able to quickly tell where parts of the program start and end when you are skimming through the code. They also explain how obscure bits of the code work. This not only helps people who have to read your code, but also helps you. Code you wrote a while ago can become very cryptic when you have to go back to modify it.

Coming out of multiple traditions, PHP allows multiple ways to put comments within its code.

#### Shell Style Comments
PHP allows Unix shell comments, which are preceded by a hash mark `#`. Shell comments are single line comments. Everything after it on that line is ignored.

```php
# a shell style comment

###############################################
# they are useful for marking off sections
# since hash marks stand out well in the code ###############################################

echo $this; # they can also occur after code
```

#### C Style Comments

##### Single Line Comments
Single line C-style comments are single line comments indicated by a double slash `//`.  Anything after the double slash is ignored.

```php
// a C-style comment

//========================================
// they don't stand out as well as hash
// marks but are more familiar to many
// people
//========================================

echo $this; // they also can occur after code
```

##### Multi-Line Comments
Multi-line C-style comments are comments meant to mark of large multi-line sections of the document. The begin and with a nested slash asterisk combination `/* */`. You should be careful using them to comment out things, since they cannot be nested.

```php
/* a C-style multi-line comment */

/* ****************************************
they are usually used to delimit large blocks **************************************** */

echo $this; /* they also can occur after code */

/* this on the other hand
/* is a mistake */
because this line isn't commented out */
```

## Variables

### Literals
We will look at some aspects of literals in more detail under data types, but here is a quick overview.  A literal is a data value that appears as itself in a program.  A literal is an expression that directly represents itself in the code. For instance, the number 2 is a numeric literal, appearing as a number in the code and representing the value of the number two.

Literals come in three flavors. These are:

- numeric literals
- string literals
- keyword literals

#### Numeric Literals
Numeric literals are numbers that appear as themselves. They may be integers or floating-point numbers. Floating point numbers may be represented with a decimal point. They may also be represented in base-10 scientific notation as [number]E[exponent], for instance, 1.75E-2.

Integers may be represented as decimal numbers or as octal (base-8) or hexadecimal (base-16) numbers.  A numeric literal integer beginning with zero is treated as an octal number.  A numeric literal integer preceded by a zero and an "x" (0x) is treated as a hexadecimal number. This means that integer numeric literals should not have leading zeros unless you want to signify a different type of enumeration that the base-10 that most people are used to.
All of the following are valid numeric literals:

- 0  -> integer
- 123 -> integer
- 1.23 -> floating point
- 0.123 -> floating point
- 1.23E5 -> scientific notation floating point
- 1.23E-7 -> scientific notation floating point
- 0123 -> octal
- 0x123 -> hexadecimal

#### String Literals
String literals are any value that appears in the code inside quotes. A string literal can be any valid character, including numbers. What makes it a string is its use in the code within single or double quote marks.

String literals can either have single or double quotes.  However, unlike some programming languages, which one you use makes a difference on PHP. Double-quoted string literals are parsed string literals while single-quoted string literals are not parsed. What this means is that single-quoted string literals are always represented exactly as entered (except for two special characters we will discuss later), while double-quoted strings can contain non-literal data to be processed at the time the program is run. In other words, PHP provides you with a way to embed variables in string literals.

#### Keyword Literals
A keyword is a word reserved by the language for its own use.  A keyword literal is a reserved word in the language that serves as representative of a single literal value. Examples of keyword literals are:

- true -> Equates to true in a conditional situation.
- false -> Equates to false in a conditional situation.
- null -> Is the value assigned to a variable that has no value. It is the value of no value.

### PHP Data Types
A data type is a general term to describe categories of values that a program or programming language can use.  A data type refers to the type of data a variable can store. PHP has eight (8) different data types you can work with.

These are…

- integer numbers
- floating point numbers
- strings
- booleans
- arrays
- objects
- resources
- null

PHP is a loosely typed language, so a variable does not need to be of a specific type and can freely move between types as demanded by the code it is being used in. But you still need to know your data types.

#### Resources And Null – The Special Cases
Resources are not an actual data type, but the storing of a reference to functions and resources external to PHP. The most common example of using the resource data type is a database call. We will not talk about them here, since they are an advanced topic.
Null is a special data type, which can have only one value, which is itself.  Which is to say, null is not only a data type, but also a keyword literal. A variable of data type null is a variable that has no value assigned to it. When a variable is created without a value, it is automatically assigned a value of null. This is so that whatever garbage was in that memory location before is cleared out. Otherwise the program may try to process it.

So why is there garbage in memory in the first place?  When computers assign a variable a value, they assign the variable a location in memory.  Then the computer stores the value in that location. The variable is really a reference to that location in memory, containing the memory address and what type of information the computer should expect to find there. It does not actually store the value, just a reference to its location. When the computer is done with the variable or is told to delete it, it does not delete the value in memory, but the reference to its location. This is far more efficient that deleting the actual values, but it means that whatever garbage was left in that location in memory is still there. This is also why you have to wrestle with pointers in programming courses, as they are how computers really work with variables and values.

Of the other two data types, we can lump everything into two categories. The first category is scalar, or primitive, data types. They are data types that can only hold a single value. These are integers, floating-point numbers, strings, and booleans. The second category is the compound data types, data types that store a collection of values. These are objects and arrays.

#### Integers
An integer is a whole number, a number with no fractional component. For those who are familiar with C, a PHP integer is the same as the long data type in C. It is a number between -2,147,483,648 and +2,147,483,647.

Integers can be written in decimal, octal, or hexadecimal. Decimal numbers are a string of digits with no leading zeros. Any integer may begin with a plus sign `+` or a minus sign `-` to indicate whether it is a positive or negative number. If there is no sign, then positive is assumed.

The decimal number system is a base ten numbering system.  This is the number system with which you are likely most familiar.  It is the number system that the human race instinctively gravitated toward.  If you are wondering why, count your fingers or your toes.

Valid decimal integers…

- 1 123 +7
- -1007395

An octal number is a base-8 number. Each digit can have a value between zero (0) and seven (7). Octal numbers are commonly used in computing because a three digit binary number can be represented as a one digit octal number. Octal numbers are preceded by a leading zero (e.g., 0123).

Valid octal integers…

- 01
- 0123
- +07
- -01007345

A hexadecimal number is a base-16 number. Each digit can have a value between zero (0) and F. Since we only have ten numbers in our numbering system (0-9), we use the letters A through F to make up the difference for hexadecimal values. Hexadecimal values are common in computing because each digit represents 4 binary numbers, which is four bits. Eight bits, or a two digit hexadecimal number, is one byte. Hexadecimal numbers are preceded by a leading zero and X (e.g., 0x123).

Valid hexadecimal integers…

- 0x1
- 0xff
- 0x1a3
- +0x7
- -0x1ab7345

So what about zero, you may ask. If anything beginning with a zero is octal then isn't zero octal? And how do we represent a decimal zero then? The answer is simple. It makes no difference. If you have zero of something, it doesn't matter how you count it, it is still zero.

If you want to find out whether a variable stores an integer you can use the `is_int()` to test whether something is an integer. If it is, then the function returns the value of true.

#### Floating Point Numbers
Floating-point numbers are also sometimes called real numbers. They are numbers that have a fractional component. Unlike basic math, all fractions are represented as decimal numbers. If you are familiar with C, PHP floating-point numbers are equivalent to the double data type. Floating-point numbers get their name from their decimal point. When using scientific notation to represent the number, the point floats in relation to the exponent being applied to the numeric component of the notation.

PHP recognizes two types of floating point numbers. The first is a simple numeric literal with a decimal point. The second is a floating-point number written in scientific notation. Scientific notation takes the form of [number]E[exponent], for example, 1.75E-2.

Some examples of valid floating-point numbers include…

- 3.14 0.001
- -1.234
- 0.314E2
- 1.234E-5
- -3.45E-3

If you want to know if a variable contains a floating-point number, you can use the `is_float()` function to test the value. If it is a floating point number, the function will return true.

#### Strings
A string is a text literal of an arbitrary length. Most of working with Web pages is about working with strings.  Being enclosed in quotes, either double or single quotes, indicates a string.

Unlike some programming languages, PHP differentiates between single and double quotes. Strings inside double quotes are parsed, or interpolated, while strings inside single quotes aren't. What this means is that if you include variables or special characters in double-quoted strings, those values are processed and become part of the string. Putting variable names and special characters in single-quoted strings causes the variable names and special character escape sequences to be written out exactly as you typed them. In other words, they are literals. This means that you can embed variables directly inside strings in PHP when using double quotes, but not when using single quotes. This make concatenating strings a little easier.

Thus we have the following situation…

```php
$myVar = "xyz";       // assign a value to $myVar
echo $myVar;          // writes 'xyz'
echo "abc to $myVar"; // writes 'abc to xyz'
echo 'abc to $myVar': // writes 'abc to $myVar'
```

This does make it easy to write PHP code out inside a string, as well as to process PHP code within a string.

##### Special Characters
Anything within quotes is part of a string, even numbers. Thus, "123" is a string, not a number. But there are special characters, which cannot be included directly in a quote. For instance, you can't have double quotes inside a double-quoted string, and you can't have single quotes inside a singe-quoted string. To include these special characters, you need to escape them so that the parser knows that they are literal characters and not string delimiters.

In PHP, you escape a character by preceding it with a backslash. There are two types of escaped characters in PHP. There are those that are a special character in the language and need to be escaped to get the parser to treat them as a literal. For instance, `\"` says that the quote after the backslash is a literal quote, and `\\` is used to include a literal backslash in a string. There are also those that are normal characters that serve as special characters when they are escaped. For instance, \n inserts a line break in the string at that location, and `\r` inserts a carriage return. Yes, they are the same thing for us, but they are different characters as far as the computer is concerned.

Line ending can be tricky.  Windows ends its lines with `\r\n`, Unix, Linux, and Mac OS X ends their lines with \n, and the Mac OS up to version 9 ends its lines with `\r`. This is why you can get garbage at the end of your lines when looking at your code in editors on a platform other than the one you wrote it in. Most code editors are smart enough to let you specify which format to save documents in.

Special characters can either be a single character preceded by a backslash or a numeric value in either octal or hexadecimal preceded by a backslash.

Some of the more common escape characters are…

- `\"` -> embeds a literal double quote in a string
- `\'`  -> embeds a literal single quote or apostrophe in a string
- `\\`  -> embeds a literal backslash in a string
- `\$` -> embeds a literal dollar sign in a string
- `\{` -> embeds a literal left brace in a string
- `\}` -> embeds a literal right brace in a string
- `\[` -> embeds a literal left bracket in a string
- `\]` -> embeds a literal right bracket in a string
- `\n` -> embeds a new line character in a string
- `\r` -> embeds a carriage return character in a string
- `\0` through `\777` -> represents and embeds any valid ASCII character value in octal format
- `\x0` through `\xff` -> represents and embeds any valid ASCII character value in hexadecimal format
- `\x0` through `\xffff` -> represents and embeds any valid Unicode character value in hexadecimal format

Strings in single quotes are not technically parsed, but you can use `\'` and `\\` to escape single quotes and backslashes in unparsed strings. No other escaped characters will work in single-quoted string literals. They will be treated as literal text.

One important thing you shouldn't have in a string is the sub-string `?>`, which ends that PHP script, even if it does occur inside a string. In fact, even `?\>` is a bad idea. It is recommended that you use the numeric value for the question mark and write it `\x3f>`. `3f` is the hex value for `?`.

You can use the `is_string()` function to test whether something is a string. If it is a string, it will return true.

PHP includes many string related functions, since much of what it does is string processing. These are discussed elsewhere.

#### Booleans
A boolean value assesses the truth value of something.  Booleans only have two values, true and false.  These two values are represented by the keyword literals of the same name. All conditionals return a true/false boolean value based on the condition being tested.
If a conditional is converted to a different data type, then true equates to one (1) and false equates to zero (0). The conversion in the other directions is a little more complex. If testing for the truth value of a non-boolean value, any of the following values will equate to false.

- The keyword literal false.
- The integer 0.
- The floating-point number 0.0.
- The empty string (""). Note, that is not a space, but a string with nothing in it.
- The string "0" (zero).
- An object with no values or methods.
- The null value.
- All other values are true, including all resource values.

#### Arrays
We will spend a lot more with arrays in a future chapter. This is just to make you aware that they exist.

An array is a variable that holds a group of values. Arrays are usually meant to store a collection of related data elements, although this is not a necessity. You access the individual elements by referring to their index position within the array. The position is either specified numerically or by name.

An array with a numeric index is commonly called an indexed array while one that has named positions is called an associative array. In PHP, all arrays are associative, but you can still use a numeric index to access them. Indexed arrays start at position zero, not at position one, so your first array element has an index of 0, and the highest position in the array is one less than the number of elements in the array.

Referencing array elements is done with the following notation…

```php
$arrayName[index];
```

You assign a value to an array position by specifying which array element you want to assign a value to:

```php
$listing[0] = "first item";
$listing[1] = "second item";
$listing[2] = "third item";
```

An individual array element can be of any type, including another array.  If you want to find out if a variable contains an array you can use the is_array() function.  We deal extensively with arrays in their own section. If you haven't gotten to it yet, beware of the fact that there are some counterintuitive elements in how PHP deals with arrays.

#### Objects
We will spend a lot more with objects in a future chapter. This is just to make you aware that they exist.

PHP is capable of functioning as an object-oriented programming language (or OOP). As such, it must be able to handle objects. An object is a data type that allows for the storage of not only data but also information on how to process that data. The data elements stored within an object are referred to as its properties, also sometimes called the attributes of the object. The code describing how to process the data is called the methods of the object.

Objects have two components to their construction. First, you must declare a class of object. It defines the structure of the object to be constructed. Then you instantiate the object, which means you declare a variable to be of a certain class and assign values to it appropriately.
Another way of looking at objects is that they allow you to create your own data types. You define the data type in the object class, and then you use the data type in instances of that class.  Yes, there is also an is_object() function to test whether a variable is on object instance.  Objects have their own section in these notes.

## Expressions
An expression is a piece of code that can be evaluated to produce a value.  The basic building block of a program is the statement. A statement is a piece of code that does something.  Statements themselves are made up of expressions and operators. An expression is a piece of code that evaluates to some value.

The simplest form of expression is a literal or a variable. A literal evaluates to itself. A variable evaluates to the value assigned to it.  For instance, any of the following are valid expressions…

- "abc"
- 123
- $a
- $x == 7
- ($a + $b) / $c

Although a literal or variable may be a valid expression, they are not expressions that do anything. The way you get expressions to do things is by linking simple expressions together with operators.
An operator combines simple expressions together into more complex expressions by creating relationships between the simple expressions that can be evaluated. For instance, if the relation you want to establish is the cumulative joining of two numeric values together, you could write `6 + 7`.

The numbers 6 and 7 are each valid expressions. The equation `6 + 7` is also a valid expression, whose value, in this case, happens to be 13.
The plus sign `+` is an operator. The numbers to either side of it are said to be its arguments, or operands. An argument or operand is something that an operator takes action on. Different operators have different types and numbers of operands. (You will also find that some operands are overloaded. This means that they will do different things in different contexts.)

Two or more expressions connected by operators are called an expression. You use operators to make complex expressions. The more sub-expressions and operators, the longer and more complex the expression, but as long as it is something that equates to a value, it is still and expression.

When expressions and operators are assembled in such a way as to produce to a piece of code that actually does something, you have a statement. Statements end in semi-colons and are the programming equivalent of the complete sentence.

For instance, `$a + $b` is an expression. It equates to something, the sum of the values of `$a` and `$b`, but it doesn't do anything. `$c = $a + $b;` is, on the other hand, a statement, because it does something. It assigns the sum of the values of `$a` and `$b` to `$c`.
Since there isn't really much to understand about expressions except for the assembly of them into compound expressions and statements using operators, we are going to look at the operators used to turn expressions into more complex expressions and statements.

### Operators
PHP has many operators and many types of operators. They can be categorized as…

- arithmetic operators
- string operators
- assignment operators
- increment and decrement operators
- casting operators
- relational operators
- logical operators
- bitwise operators
- a few others that don't really fit into any category

Except for bitwise operators, we are going to look at all of these in more detail. Bitwise operators allow you to manipulate integer values at the binary level. This is not something you will need for anything but the most advanced PHP programs. Bitwise operations also require a strong grounding in computer logic at the level of logic gates, registers and memory addressing. We are going to stick with things you can make use of almost immediately.

When working with operators, you must be careful about paying attention to four aspects of the operator…

- number of operands
- type of operands
- order of precedence
- operator associativity

### Number of Operands
Different operators take different numbers of operands. Most operators are binary operators, which means they are used to combine two expressions into a single, more complex expression. We are most familiar with binary operators since most mathematical operators are binary operators, for instance `$a + $b` or `$c / $d`.

Some operators are unary operators. This means that they only take one operand. For instance, the negation operator `-` turns a numeric value into its negative value `-7`. PHP also has increment and decrement as in C and C++ operators, which are unary operators.

There is one ternary operator in PHP, which is a shorthand form of the conditional statement. We will discuss it when we talk about conditional expressions.

### Types of Operands
When working with operators, you should pay attention to the type of operand an operator is meant to work on. Certain types of operators expect their operands to be of certain data types. Unlike some programming languages, PHP will try to convert the operands associated with an operator to the type of operand the operator is expecting. For instance, mathematical operators only work on numbers. Even though PHP will try to convert non-numeric values to numeric values for you, it still can't multiply two strings together if they are not numbers. `"abc" * "def"` is not a valid expression.

This process of converting from one type to another is known as casting. PHP will try to take care of casting for you. This process is known as implicit casting. Different operators have different rules for how they cast their operands. You can also explicitly cast operands. This is discussed a little later.

Some operators are overloaded. An overloaded operator does different things in different contexts. For instance, the period `.` is a concatenation operator for strings, but is also the decimal point for floating point numbers and the separator between object names and property names.

Some binary operators only accept certain values as their left hand operator. This is true of most of the assignment operators, which assign the value that is the result of the expression on the right to the expression on the left. This means that the expression on the left has to be something you can assign a value to.

The left-hand expression in assignment operations is known as an L-value. An L-value is, simply, an expression that occurs on the left hand side of an assignment operator. An L-value expression must be an expression that can legitimately have a value assigned to it. The only valid L-values in PHP are variables, properties of objects, and elements of arrays.

```php
// A legal PHP expression
$a = $b + $c;

// An illegal PHP expression
// You cannot use the assignment operator to
// assign a value to a complex expression
$a + $b = $c;

// A pointlessly complex, but legal expression
// The parentheses create a specific order of
// precedence, which is our next topic
$a = $b + ($c = $d / ($e = $f * $g));
```

### Order Of Precedence
The order of precedence is the order in which operators are acted upon.  Operators have an order or precedence, or an order in which they are processed in an expression. For instance, multiplication and division take precedence over addition and subtraction and everything else being equal will be processed first.

Operators that have the same precedence are processed in the order in which they appear in the expression. For instance, addition and subtraction have the same order of precedence, and so are processed in the order in which they appear.
Most operators that have the same precedence as one or another either normally only occur once in an expression or can be processed in any order in relation to each other. With addition and subtraction, if you start with 10 it does not matter whether you add 5 and subtract 3, or subtract 3 and add 5, the result is still 12.

You can use parentheses within an expression to clarify or override the default order of precedence.  Using parentheses to mark of the order the expression would be processed in anyway makes the code easier to read. It doesn't change the order of processing, but it does clarify it.
Overriding the order of precedence means you want the operators to be processed in an order different from the default order.  Operators with the same precedence can occur in any order without affecting the result.

```php
// $a == 12
$a = 10 + 5 - 3;

// $b == 12
10 - 3 + 5;

//$c == 4
$c = 10 * 2 / 5;

//$d ==4
$d = 10 / 5 * 2;
```

Operators with different orders of precedence must occur in a specific order or the results will be different.

```php
// default order $a = 20
$a = 10 + 5 * 2;

// same, with order specified $b = 20
$b = 10 + (5 * 2);

// order changed $c = 30
$c = (10 + 5) * 2;
```

For basic math, the operators with the highest order of precedence are multiplication and division, and the lowest is the assignment operator. The reality of programming is a bit more complex.

Here is a partial list of all operators in PHP by order of precedence. The list is in descending order, from highest to lowest. Operators in the same grouping have the same level of precedence. (The Associativity column lists those that are right to left, instead of left to right. See the next section for an explanation of this.)

The grouping numbers are entirely arbitrary and are just meant to make the table easier to read in print form.   You can find this table on the web here…

**Operator Precedence**

| Associativity | Operators |
|---------------|-----------|
| non-associative | `clone` `new` |
| left | `[` |
| right | `**` |
| right | `++` `--` `~` `(int)` `(float)` `(string)` `(array)` `(object)` `(bool)` `@` |
| non-associative | `instanceof` |
| right | `!` |
| left | `*` `/` `%` |
| left | `+` `-` `.` |
| left | `<<` `>>` |
| non-associative | `<` `<=` `>` `>=` |
| non-associative | `==` `!=` `===` `!==` `<>` |
| left | `&` |
| left | `^` |
| left | `|` |
| left | `&&` |
| left | `||` |
| left | `? :` |
| right | `=` `+=` `-=` `*=` `**=` `/=` `.=` `%=` `&=` `|=` `^=` `<<=` `>>=` `=>` |
| left | `and` |
| left | `xor` |
| left | `or` |
| left | `,` |

### Associativity
All operators have associativity. Associativity is the direction in which the operator is processed.  Most operators have left to right associativity, which is to say that they are processed from left to right. In the expression $a + $b - $c;, $a and $b are added together and then $c is subtracted from the result.
Some operators have right to left associativity. The most common of these is the assignment operator. For instance, in the expression $a = $b = $c;, the value of $b is set to the value of $c, then the value of $a is set to the value of $b. Looking at the code, you would expect all three values to be equal, and this is what the expression does. If left to right associativity were used for assignment, this would not be the case.
ARITHMETIC OPERATORS
Arithmetic operators fall into two categories, those that modify the value of an expression or set of expressions and those that take the value of one expression and assign it to another expression. These latter operators are also called assignment operators.
The following arithmetic operators are the basic math operators. They do not alter the values of their operands, and therefore need to have their result assigned to some variable in order to have any real effect.

- Addition `+` -> The addition operator adds two numeric operands or concatenates two string operands. Values need to be convertible to a number to work with the addition operator.
- Subtraction `-` -> The subtraction operator subtracts the value of the second operand (the one after the minus sign) from the value of the first operand (the one before the minus sign). It only works on numbers.
- Multiplication `*` -> The multiplication operator multiplies the numeric values of two operands together.
- Division `/` -> The division operator divides its first operand by its second operand. Division of integers that do not divide evenly will yield a floating-point result. Division by zero yields Infinity or -Infinity. The expression 0/0 evaluates to Nan.
- Modulo `%` -> The modulo operator divides its first operand by its second and returns the modulus. The modulus in division is the remainder, or what is left over.
- Unary Minus `-` -> The unary minus is a unary operator that negates the operand immediately following it, which is to say, converts it to its negative equivalent.
- Unary Plus `+` -> This operand does nothing, but exists to balance the unary minus.

The following arithmetic operators are unary operators that modify the value of their single operand.

- Increment `++` -> The increment operator increments the numeric value of its operand by one. If placed before the operand, it returns the incremented value. If placed after the operand, it returns the original value and then increments the operand.
- Decrement `--` -> The decrement operator decrements the numeric value of its operand by one. In other words, it counts backwards. If placed before the operand, it returns the decremented value. If placed after the operand, it returns the original value and then decrements the operand.

Unlike some languages, PHP allows you to increment certain strings as well as integers. Thus, the following code is legal.

```php
$i = 'a';
$i++;
```

The incrementing and decrementing works with strings and numbers is as follows…

- All numbers are either incremented or decremented by one each time the statement is invoked. Once a digit reaches a value of nine, it rolls back over to zero and the one is carried left to the next position. If it is decremented to zero, it rolls over to nine and one is subtracted from the position to the left.
- All letters in the range of A through Z, either upper or lower case, are incremented or decremented by one each time the statement is invoked. Thus 'A'++ would become 'B', and so forth. When a given character reaches a value of 'Z' it is rolled back over to 'A' and the one is carried left to the next position. If it is decremented to 'A', it rolls over to 'Z' and one is subtracted from the position to the left.
- This even works for mixed strings.

Increment and decrement examples…

```php
// result '4'
'5'--

// result 'F'
'E'++

// result 'xza'
'xyz'++

// result 'xZa'
'xYz'++

// result 'M0'
'L9'++

// result '11z'
'12a'--
```

The rest of the arithmetic operators are assignment operators. They assign the value of the operand on the right to the operand on the left. There are two types of assignment operators. The first is the simple assignment operator. It is represented by the single equals sign `=`. It is the assignment operator we are most familiar with.

The value to the left of the assignment operator must be an L-value, which is an expression that can have a value assigned to it.

```php
$a = $b + c$;
$validCheck = ($testVar == $myCond);
```

PHP also allows another type of operator that perform with is called assignment with operation. What this means is that they include both a math operator and an assignment operator in one operation. What is the purpose of such an operator? Well, many expressions you will end up writing may take the form of $a = $a + $b;, or the value of the first operand equals the value of the first operand as modified by a second operand. PHP allows a shorthand notation for these. $`a = $a + $b;` is equivalent to `$a += $b`. The same shortcut can be applied to subtraction, multiplication, division and modulus.

- `$a += $b;` is the same as `$a = $a + $b;`
- `$a -= $b;` is the same as `$a = $a - $b;`
- `$a *= $b;` is the same as `$a = $a * $b;`
- `$a /= $b;` is the same as `$a = $a / $b;`
- `$a %= $b;` is the same as `$a = $a % $b;`

Note that in each of these, the two characters form a single operator, and cannot have a space between them.

### Relational Operators
Relational operators allow you to test the relationship between two operands. They can test for equality between operands. They can compare operands to determine the relationship between them. There are even relational operators that test whether one operand is a property of another or of a given class of object.

The first relational operator you should know about is the equality operator.  The equality operator is represented by the double equals sign `==` It is used to assess whether two operands have the same value. If they do, then it returns a value of true. Otherwise it returns a value of false.

The equality operator will do data type conversion if necessary.  All of the following statements equate to true…

```php
'1' == '1'
'1' ==  1
'1' == true
// true equals one when converted to a number
```

Note that objects and arrays are compared by reference. Two objects are only equal if they are both references to the same object. If you want to test the properties of two different objects for equality, then you have to test the properties themselves, not the object.
Different arrays are never equal, even if they contain the same information. If you want to test the elements of the arrays for equality, you have to test the individual elements.

There is also an identity operator, represented by a triple equals sign `===`, which only equates to true when both operands have the same value and are of the same type.

```php
'1' === '1'   // true
'1' ===  1    // false
'1' === true  // false
```

Equality operators also have their opposites.  The inequality operator `!=` returns true where equality would return false. The non-identity operator ( !== ) returns true where identity would return false.

```php
'1' !== '1'   // false
'1' !==  1    // true
'1' != '2'    // true
'1' != '1'    // false
```

The next types of relational operators are the comparison operators. Comparison operators test the relationship, or relative order, of two values. These are:

- less than `<`
- greater than `>`
- less than or equal to `<=`
- greater than or equal to `>=`

### String Operators
There is really only one specific string operator, although the string object has many methods you can access.
The only string operator is the concatenation operator. It is represented by the period `.`. The concatenation is a special case of operator. It is an overloaded operator, since it serves more than once function depending on context. It concatenates strings, but it also serves as a decimal point and a separator for object property relationships.

When working with strings, the comparison operators test on a character-by-character basis, so two strings that are the same except for some trailing spaces, or a difference in capitalization, will be treated as different strings. This means that comparisons can get confusing. This is especially true of strings that contain numeric values.

```php
// compare two numeric strings compared as number to number
'11' < '3'       // false

// compare a numeric string and a number compared as number to number
'11' < 3        // false

// compare a non-numeric string to a number compared as a number
// 0 (or no number) is less than 3
'eleven' < 3    // true

// compare a non-numeric strings compared as a string
'eleven' < 'three'    // true

// compare a numeric string to a non-numeric string
// compare as a string ACSCII 'e' is greater than ASCII '3'
'eleven' < '3'  // false
```

### Logical Operators
There are four logical operators. Logical operators work with boolean values. The double characters for AND and OR are important, otherwise the operators mean something else.

- Logical AND `&&` or `and` -> The logical AND (double ampersands) compares two boolean operands and equates to true if they are both true.
- logical OR `||` or `or` -> The logical OR (double vertical bars) compares two boolean operands and equates to true if either one is true.
- logical XOR `xor` -> The logical XOR compares two boolean operands and equates to true if one and only one is true. The logical XOR does not have a symbolic construct in PHP, however, it can be simulated with `(a || b) && (!(a && b))`
- logical NOT `!` -> The logical NOT (exclamation point) negates the value of boolean operand, which is to say it returns true if the operand has a value of false.

Note that `and`, `xor`, and `or` have a significantly different position in order of precedence than `&&` and `||` do. Logical operators, without parentheses, will be processed in the following order…

- !
- &&
- ||
- and
- xor
- or

The fact that an `and` operator and an `or` operator occur twice at different points in the order of precedence can be useful in complex statements that include conditionals.

Since the expressions are evaluated in order, you can speed processing time of your scripts by coding the operand most likely to be the deciding factor first. For logical AND, if either one is false, than it returns false. Therefore, the operand most likely to be false should come first. For logical `or`, if either is true, it returns true, so it makes sense to put the operand most likely to be true first.

Note that when this happens, the second operand never gets evaluated. This is known as “short-circuit evaluation”.  This means you should not have any value changes in the second that may affect other parts of the code, since the expressions in the second operand may not get executed.

### Casting Operators
Although PHP handles implicit casting, there are times when you may want to determine the data type of a given variable or even specify the type you want to cast a variable to. PHP has two functions and some operators to help you with this.

### `gettype()` and `settype()`
`gettype()` and `settype()` allow you to determine the data type of a variable and set the data type of a variable, respectively.
`gettype()` returns a string that represents the name of that data type. In order to access that value, you either need to assign it to something or echo the result of the function.

```php
$result = gettype($mysterymeat);
echo gettype($whoknows);
```

`settype()` takes two arguments. The first is the variable to be cast. The second is a string representing the name of the data type to be cast to. The data type names are the same as the names of the casting operators below. So to cast something to an integer, you could use the string "integer" or "int". The `settype()` function changes the type of the variable it is passed, it does not return a new value of that type.

```php
settype($myNum, "string");
settype($myStr, "float");
```

The casting operators also allow you to cast variables to new types. Unlike the settype function, they return a value that is the value of the variable cast in the new type. The operator is used with the assignment operator as follows:

```php
$result = (operator) $original;
$res = (integer) $myStr;
```

The casting operators are…

- `(int)` or `(integer)` to cast to an integer
- `(float)` or `(real)` to cast to a floating-point number
- `(string)` to cast to a string
- `(bool)` or `(boolean)` to cast to a boolean
- `(array)` to cast to an array
- `(object)` to cast to an object

Be aware of the fact that casting will may change the value of the variable as well as its type. For instance, casting a floating-point number to an integer will truncate any fractional part.

```php
$a = (int) 4.1715   // $a == 4
$b = (int) "123abc" // $b == 123
```

Some casts may also not produce any meaningful results. For instance, casting an array to a string yields a string whose value is "array". However, you can switch back and forth between arrays and objects freely with the index values becoming the properties. If properties of the array cannot be cast to object properties, PHP will even keep those values so that they will be restored when the variable is cast back to an array. This most commonly occurs because it is possible to have index names that are not valid property names.

### A Few More Operators
There are just three more operators worth mentioning right now.

The ampersand `&` before a variable `&$abc` overrides pass by value to specify that you want to pass the variable by reference instead. The ampersand is an overloaded operator and character in PHP, so use carefully.

The at sign `@` before an operator or function call tells PHP to not report any errors from it should any errors arise.

The backtick, or grave accent `` ` `` , can be used to define a string as a command to be passed to the server. The string is executed as a command and its results are returned.

```php
$dirListing = `ls -l`;
```

## Advanced Output
One of the most commonly used features of PHP is to write content out for display over the Web. It can take data from most any data source and with proper coding format it for display in a Web browser.

PHP is designed to run on the server, behind the scenes. Not only should it not display in the Web browser window, but if someone views the source code for a PHP generated document that is currently displayed in their Web browser, the code should not be visible there either. Unless there is an error and the subsequent generation of an error message, a user should never see the PHP code. The PHP code is stripped from the document before it is sent to the user.

The way PHP works in a Web document is by treating the document it is embedded in as an output file. It inserts it output at the location in the code where the script is place. In other words, the output from the script replaces the script before the document is sent on to the user.

We have already encountered one way to do this sort of dynamic document generation with PHP using the `echo` statement. It echoes the content back to the current document. But PHP has more ways to write output than that. The statements used to write content back to the document in PHP is as follows:

- `echo`
- `print()`
- `printf()`
- `sprintf()`
- `print_r()`
- `heredoc`
- `nowdoc`
- `var_dump()`

### Echo
Echo is perhaps the most common command for writing output back to the containing document for transmission to the client. Unlike the other print commands, it is not a function. Rather it is a language construct. In other words it is a command that is used like an operator, rather than a function.

You will often see echo written to look like a function call, with parentheses after it, echo ($someVar);. The parentheses help to organize the code and are useful for marking the limits of longer strings and concatenations, but the parentheses are optional, and are even not allowed in some circumstances.

The echo command writes the values of one or more arguments to the screen. If there is more than one argument, then the arguments must occur in a comma separated list. Although the individual elements can have parentheses around them for grouping, the entire list cannot. This is, incidentally, because parentheses have a higher order of precedence than the echo command, so the parser would try to parse the comma separated list as an expression and pass the results to the command.

Correctly formed echo commands…

```php
echo $myVar;
echo ($myVar);
echo $myVar, $myOtherVar;
echo ($myVar), ($myOtherVar);
```

Incorrectly formed echo commands…

```php
// parentheses can’t be used this way
echo ($myVar, $myOtherVar);

// needs a separator between arguments
echo $myVar $myOtherVar;

// wrong separator between arguments
echo $myVar; $myOtherVar;
```

The echo command writes out the arguments to the document in the order in which they occur in the statement.

### Print
The print command is not a proper function.  It is a language construct.  Unlike the echo command, it only takes a single argument. This argument is written out to the document being processed.

### Formatting Output
PHP allows two variations on the C-style `printf()` commands, the `printf()` command itself and the `sprintf()`. Both allow you to format output strings based on formatting arguments passed to the function. Thus you can do things like specify alignment, padding characters, precision, and numbering system to display with.

The `sprintf()` command does the same thing as the `printf()` command, except that instead of return the results to the output document, it returns the results to be assigned to some variable. This allows you to then use the formatted output string in echo and print statements. So aside from a coding example, nothing more needs to be said about it.

```php
$myOut = sprintf('%.2f', $myNum);
echo "This number has two decimal places: " . $myOut;
```

So how does `printf()` work? It works by taking two or more arguments, which determine how the output string is to be generated. The first argument is the formatting string, which is a template that specifies how the output is to be formatted. The second argument and all other arguments after the second are data elements to be inserted into the output string where specified in the formatting string.

```php
printf('template', 'data'[...]);
printf('%d equal %x hex', 200, 200);
printf('%0.6f', $fpNum);
```

The purpose of the `printf()` statement is to format output for display. Since we are talking about PHP in the context of web development, its most common use for us is to format floating point numbers, but it has a wide variety of uses…

- Displaying integers in decimal, octal, or hexadecimal format.
- Insert values into string literals.
- Specify the sign of values.
- Set precision (the number of decimal places) in floating point numbers.
- Round floating point numbers.
- Set fixed width data fields.

The key element in the `printf()` statement is the formatting string. It contains one or more substation markers that specify what to do with the arguments that follow the formatting string. There should be one data element for each substitution marker. Each substitution maker begins with a percent sign ( % ) and ends with a character that indicates the display type for the data. Between the percent sign and the display type there can be a series of formatting modifiers that specify the formatting features of the output string.

### Formatting Modifiers
The formatting modifier change how the formatted output element is displayed. They are not required if the default settings are satisfactory for a given display type are satisfactory. If they are included, they must occur in the following order.

#### Padding Character
Sometimes you want to format elements so that they have some padding before or after them. The padding character allows you to specify what this is. The length and precision of the string are defined later. The padding character can have the following values…

- 0 (zero) -- a zero in this position indicates that the content, presumably a number, should be padded with leading zeros if shorter than the minimum display length or with trailing zeros if the precision is greater than the actual number of values after the decimal place. If you do not specify a length or a precision, then no padding will take place.
- (a blank space) -- a blank space in this position indicates that padding should be done with spaces. This is the default, so you don't actually have to specify it.
- 'x -- a single quote followed by some character specifies the character after the quote as being the padding character. In this case, the X would be a padding character.

#### Sign
The sign indicator is not exactly what it seems. What it does depends on the sign use. A minus sign `-` right justifies the output string, assuming the string is shorter than the specified length. A plus sign `+` forces a leading plus sign to appear in front of positive numbers.

#### Length
The length is a number that represents the minimum number of characters to output. The string will be padded to fit. The direction of the padding depends on the data type and the sign operator.

#### Precision
Precision only applies to floating point numbers and is used to specify how many positions to specify after the decimal place. It is represented by a period followed by a number representing the number of places desired.

An example using all of the formatting modifiers in a single statement…

```php
printf('The answer is %0+6.4f', $result);
```

Another example:

```php
printf("% 15S %'.-25d", $title, $page);
// which by the way would print the following
// for a table of contents or similar
// Some Title     .......................##
```

Also, if the percent sign is an operator in this situation, then how do you print a percent sign? You do this by putting two percent signs in the formatting string where you want the percent to occur.

```php
printf('%d%%', 25); // results is "25%"
```

#### Type Specifiers
The type specifier allows you to specify the data type the output string is supposed to represent. The data type of the output is actually a string, but the type specifier allows you to specify that the formatting in the string be appropriate to a given data type. For instance, you can specify that the output from the substitution be formatted as an integer, or a hexadecimal number, or a floating-point number with or without scientific format.

The type specifier must always be the last character as that it terminates the substitution string. Its values are as follows:

#### Strings
There is only one string specifier, S. The letter is capitalized. It is used to print out non-numeric values.

#### Integers
To display integers, any of the following values can be used…

- d -> display a decimal integer
- I -> display as decimal integer
- U -> display as unsigned integer
- B -> display as a binary value
- O (capital letter O) -> display as an octal value
- x -> display as a hexadecimal value with lower case letters
- X -> display as a hexadecimal value with upper case letters

#### Floating-Point Numbers
To display floating-point numbers any of the following can be used…

- f -> display as a floating-point number in standard decimal notation
- E -> display as floating-point number in scientific notation
- e -> same
- G -> if the requested precision is greater than or equal to the precision of the value to be written, then use standard decimal notation, otherwise use scientific notation
- g -> same

### Here Documents
The heredoc string structure is a method of including larger strings inside your code. You can use it to include content of any length. To create a heredoc, you use a special operator that is made up of three less than symbols `<<<`. The syntax is as follows…

```php
$longString = <<< termination_marker
any amount of content
termination_marker;
```

For instance…

```php
$longFellowNot = <<< End_of_verse
This short poem
May not fill a tome,
But it serves to show
How it is that heredoc goes.
End_of_verse;
```

Anything between the termination markers is preserved, included all white space, quote marks, and special characters. The last carriage return before the closing termination marker is omitted, so if you want one, you should leave a blank line after the end of the content and before the termination marker.  You just need to make sure that your termination string does not occur anywhere in the content being delimited.

Heredoc will also process the internal herdoc for variables.

An expample would be…

```php
$foo = new foo();
$name = 'MyName';

echo <<<EOT
My name is "$name". I am printing some $foo->foo.
Now, I am printing some {$foo->bar[1]}.
This should print a capital 'A': \x41
EOT;
```

The preceding would output the following…

> My name is "MyName". I am printing some Foo.
> Now, I am printing some Bar2.
> This should print a capital 'A': A

#### Now Documents

The books talks about heredoc on pages 51 - 52. In more recent versions of PHP[^1], there is a construct called the [nowdoc](http://php.net/manual/en/language.types.string.php#language.types.string.syntax.nowdoc). The syntax is subtly different. A nowdoc uses single quotes instead of double. It holds several advantages over the heredoc. The best example of this is that nowdoc, unlike a heredoc, will not process embedded code within the construct. This is useful if you are outputting code as it alleviates the code escape requirements of the heredoc.

```php
<?php
$foo = new foo();
$name = 'MyName';

echo <<<'EOT'
My name is "$name". I am printing some $foo->foo.
Now, I am printing some {$foo->bar[1]}.
This should not print a capital 'A': \x41
EOT;
?>
```
The preceding would output the following…

> My name is "$name". I am printing some $foo->foo.
> Now, I am printing some {$foo->bar[1]}.
> This should not print a capital 'A': \x41

### Data Dumps
Sometimes you are writing code that is not meant to format something nicely for the screen, but rather to display the values of elements within the code so that you can debug or track your scripts. PHP provides two commands to do this, `print_r()` and `var_dump()`.
Both attempt to display any variable passed to it, including arrays and objects, in a meaningful fashion. The other output statements will just print the string "Array" for arrays and "Object" for objects.

If you are using `print_r()` on an array, be aware of the fact that it does move the pointer indicating current array position to the end of the array. So of you are going to use that array later in the code, it will need to be reset.

Also, be careful not to use `print_r()` if there is any chance of the structure you are referencing might be recursive. Some objects do contain references back to themselves. This will yield an infinite loop. `var_dump()` is a little smarter. If it finds itself recursing, it stops after the third iteration.

What follows is a comparison of outputs for the different output statements (excluding `printf()`) so you can see how the deal with different data types. Note that if you use `print_r()` or `var_dump()` to write to a Web page, you need to put the output in `<pre>` tags to look like this, otherwise it will run together. This is because, as with anything in an HTML document, white space is ignored unless the browser is told otherwise.

What is represented here is the output of…

- a boolean,
- a floating-point number,
- a string,
- an array,
- and an object

These are our test variables:

```php
// a boolean
$testB = true;

// a floating-point number
$testN = 1.21715e12;

// a string
$testS = 'a test string';

// an array
$testA = array(1, 2, 3, 'cat', 'dog', 'bird');

// an object
class someObj {
   var $a = 10;
   var $b = '2';
   function ret_20() { return ($this->a * $this->b); }
} $testO = new someObj;
```

Output from echo

```php
// a boolean
1

// a floating-point number
1.21715E+012

// a string
a test string

// an array
Array

// an object
Object

Output from print
// a boolean
1

// a floating-point number
1.21715E+012

// a string
a test string

// an array
Array

// an object
Object

Output from print_r()
// a boolean
1

// a floating-point number
1.21715E+012

// a string
a test string

// an array
Array
   (
       [0] => 1
       [1] => 2
       [2] => 3
       [3] => cat
       [4] => dog
       [5] => bird
   )

// an object
someobj Object
   (
       [a] => 10
       [b] => 2
   )

Output from var_dump()
// a boolean
bool(true)

// a floating-point number
float(1.21715E+12)

// a string
string(13) "a test string"

// an array
array(6) {
     [0]=>
     int(1)
     [1]=>
     int(2)
     [2]=>
     int(3)
     [3]=>
     string(3) "cat"
     [4]=>
     string(3) "dog"
     [5]=>
     string(4) "bird"
   }

// an object
object(someobj)(2) {
     ["a"]=>
     int(10)
     ["b"]=>
     string(1) "2"
   }
```

[^1]: PHP 5.3 and newer