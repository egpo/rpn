rpn - Reverse Polish notation PHP class
===
This PHP class implements a Reverse Polish notation (RPN) evaluation that supports numeric, strings and user defined functions as well as built-in PHP functions for numeric/string manipulation.

#####Live samples and other projects can be found on my [development] (http://dev.egpo.net/rpn) site.

##### Some Examples:
##### 1. A numeric example:
- Expression:  "5 + ((1 + 2) * 4) − 3"

######RPN representation:
- 5 1 2 + 4 * + 3 -

The result of this example is **14** and is calculated in the following manner:

1. 1+2 = 3
2. 3*4 = 12
3. 12+5 = 17
4. 17-3 = **14**

```
require_once('rpn.php');
$rpn = new RPN();
$res = $rpn->rpn("5 + ((1 + 2) * 4) - 3");
```

##### 2. A 'date' and 'strtotime' functions example:
- Expression: "'Now is: '+date('Y-m-d H:i:s',strtotime('Now'))"

######RPN representation:
- 'Now is: ' 'Y-m-d H:i:s' 'Now' strtotime date_ +

The result of this example is **Now is: 2014-01-05 13:13:20:09** and is formed in this way:

1. strtotime('Now') = 1388928430
2. date_2('Y-m-d H:i:s', 1388928430) = '2014-01-05 13:27:10'
3.  'Now is: ' + '2014-01-05 13:27:10' = **'Now is: 2014-01-05 13:20:09'**

```
require_once('rpn.php');
$rpn = new RPN();
$res = $rpn->rpn("'Now is: '+date('Y-m-d H:i:s',strtotime('Now'))");
```

##### 3. A string example:
- Expression:  "'This is an '+upper('example')+' of a RPN '+lower('STATEMENT')"

######RPN representation:
- 'This is an ' 'example' upper + ' of a RPN ' + 'STATEMENT' lower +

The result of this example is **This is an EXAMPLE of a RPN statement** and is formed in this way:

1. upper('example') === strtoupper('example') = 'EXAMPLE'
2. 'This is an ' + 'EXAMPLE' = 'This is an EXAMPLE'
3. 'This is an EXAMPLE' + ' of a RPN ' = 'This is an EXAMPLE of a RPN '
4. lower('STATEMENT') === strtolower('STATEMENT') = 'statement'
5. 'This is an EXAMPLE of a RPN ' + 'statement' = **'This is an EXAMPLE of a RPN statement'**

```
require_once('rpn.php');
$rpn = new RPN();
$res = $rpn->rpn("'Now is: '+date('Y-m-d H:i:s',strtotime('Now'))");
```

Definition
---
From wikipedia: **Reverse Polish Notation (RPN)** is a mathematical notation in which every operator follows all of its operands. It is also known as postfix notation and is parenthesis-free as long as operator arities are fixed. The description "Polish" refers to the nationality of logician Jan Łukasiewicz, who invented (prefix) Polish notation in the 1920s. For more info, please visit [wikipedia] (http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Class Variables
---
A copy of the input string of the last RPN calculation:
```
public $input='';
```
The Reverse Polish notation conversion:
```
public $rpn='';
```
The result of the Polish Notation calculation:
```
public $res='';
```
An array of the supported operators available for calculation with their weight prec·e·dence:
```
private $operators = array('^' => 1, '*' => 2, '/' => 2, '+' => 3, '-' => 3);
```
Array with all the available functions, including the user defined functions and the PHP internal functions:
```
private $functions;
```
Internal array built for faster execution of the RPN calculation:
```
private $rpnar;
```

Class Methods
---
1. Main RPN processing method:
Performs the RPN conversion and calculation.
- Input: $string - has the statement to be calculated, can be a numeric or a string
- Output: The result of the calculation

```
function rpn($string){...}
```

2. Register a user defined function:
The function can accept any number of parameters.
- Input: 
  - $function - function name used in the Reverse Polish Notation input
  - $callback - name of the function to call for processing, user defined of internal function
  - $minparams - minimum parameters the function receives
  - $maxparams - maximum parameters the function can receive
- Output: true / false

```
function register($function, $callback, $minparams, $maxparams=null){...}
```

Use the `printf()` function.
``There is a literal backtick (`) here.``


`code`
``code``
block quote
> one
> two
> three

In this README
function rpn($string)


