Download Link: https://assignmentchef.com/product/solved-cs112-programming-assignment-2-expression-evaluation
<br>
<strong>In this assignment you will implement a program to evaluate an arithmetic expression</strong>

<h1>Expressions</h1>

Here are some sample expressions of the kind your program will evaluate:

3

Xyz    3-4*5

a-(b+A[B[2]])*d+3

A[2*(a+b)]

(varx + vary*varz[(vara+varb[(a+b)*33])])/55

The expressions will be restricted to the following components:

Integer constants

Simple (non-array) variables with integer values

Arrays of integers, indexed with a constant or a subexpression

Addition, subtraction, multiplication, and division operators, i.e. ‘+’,’-‘,’*’,’/’ Parenthesized subexpressions

Note the following:

Subexpressions (including indexes into arrays between ‘[‘ and ‘]’) may be nested to any level

Multiplication and division have higher precedence than addition and subtraction

Variable names (either simple variables or arrays) will be made up of one or more letters ONLY (nothing but letters a-z and A-Z), are case sensitive (Xyz is different from xyz) and will be unique. Integer constants may have multiple digits

There may any number of spaces or tabs between any pair of tokens in the expression. Tokens are variable names, constants, parentheses, square brackets, and operators.

<h1>Implementation and Grading</h1>

On the Autolab assignment page, you will you will see a file named expression_project.zip, which is an Eclipse project file. Download it to your computer, then follow the instructions on the Eclipse page under the section “Importing a Zipped Project into Eclipse” to get the entire project into your Eclipse workspace.

You will see a project called Expression Evaluation with the following classes in package app:

Variable

This class represents a simple variable with a single value. Your implementation will create one Variable object for every simple variable in the expression (even if there are multiple occurrences of the same variable). You don’t have to implement anything in this class, so <strong>do not make any changes to it.</strong>

Array

This class represents an array of integer values. Your implementation will create one Array object for every array in the expression (even if there are multiple occurrences of the same array). You don’t have to implement anything in this class, so <strong>do not make any changes to it.</strong>

Expression

This class consists of methods for various steps of the evaluation process:

<ol>

 <li><strong>20 pts</strong>: makeVariableLists – This method populates the vars and arrays lists with Variable and Array objects, respectively, for the simple variable and arrays that appear in the expression.</li>

</ol>

You will fill in the implementation of this method. Make sure to read the comments above the method header to get more details.

<ol start="2">

 <li>loadVariableValues – This method reads values for all simple variables and arrays arrays from a file, into the Variable and Array objects stored in the vars and arrays array lists. This method is already implemented, <strong>do not make any changes</strong>.</li>

 <li><strong>60 pts</strong>: evaluate – This method evaluates the expression. You will fill in the implementation of this method.</li>

</ol>

Evaluator, the application driver, which calls methods in Expression. You may use this to test your implementation. There are two sample test files etest1.txt and etest2.txt, appearing directly under the project folder.

You are also given the following class in package structures:

Stack, to be (optionally) used in the evaluation process

Do not add any other classes. In particular, if you wish to use stacks in your evaluation implementation do NOT use your own stack class, ONLY use the one you are given. The reason is, we will be using this same Stack class when we test your implementation.




<strong>Notes on tokenizing the expression</strong>

You will need to separate out (“tokenize”) the components of the expression in makeVariableLists and evaluate. Tokens include operands (variables and constants), operators (‘+’,’-‘,’*’,’/’), parentheses and square brackets.

It may be helpful (but you are not required) to use java.util.StringTokenizer to tokenize the expression. The delims field in the Expression class may be used in the tokenizing process.

The <a href="https://docs.oracle.com/javase/8/docs/api/java/util/StringTokenizer.html">documentation</a> of the StringTokenizer class says this:

“StringTokenizer is a legacy class that is retained for compatibility reasons although its use is discouraged in new code. It is recommended that anyone seeking this functionality use the split method of String or the java.util.regex package instead.”

For the purpose of this assignment, you may use StringTokenizer without issue. Alternatively, you may use the split method of the String class, or the Pattern and Matcher classes in the package java.util.regex.

Or, you may simply parse the expression by scanning it a character at a time.




<strong>Rules of implementation!</strong>:

You may NOT modify any of the files except Expression.java in <strong>ANY</strong> way.

You may NOT make <strong>ANY</strong> modifications to Expression.java EXCEPT:

Write in the bodies of the methods you are asked to implement,

Add private helper methods as needed (including the recursive evaluate method discussed below.)

Note that the java.io.*, java.util.*, and java.util.regex.* import statements at the top of the file allow for using ANY class in java.io, java.util, and java.util.regex without additional specification or qualification.




<strong>Guidelines and recommendations for implementing </strong><strong>evaluate</strong>

Recursion (optional) for sub-expressions in parentheses

While recursion is optional for this assignment, using it to evaluate subexpressions will make it a LOT easier to write working code. (This is a great opportunity to learn how to use recursion in a realistic situation!!)

There are a couple of coding options if you want to use recursion:

One option is to make the public evaluate method itself recursive. So, for instance, if the main expression is

a-(b+A[B[2]])*d+3

01234567891111111  (these are the positions of the characters in the expression)

0123456

then, to recursively evaluate the subexpression in parentheses, you may call the recursive evaluate method like this:

float res = evaluate(expr.substring(3,11), vars, arrays);

Another option is to write a separate private recursive evaluate method, with two indexes that mark the start and end of the subexpression in the main expression. Then, for the above example, you can call the recursive method like this:

float res = evaluate(expr, 3, 11, vars, arrays);

(The expr parameter is the original expression for every call.)

And, to start with, you may call the recursive evaluate method from the public evaluate method like this:

return evaluate(expr, 0, expr.length()-1, vars, arrays);

which is the entire expression.

You will need to use this second option if you want to include other parameters in your recursive evaluate.

In either case, the auto grader will call the public evaluate method.

Recursion (optional) for array index expressions (within ‘[ and ‘]’), using the same approach as above.

A stack may be used to store the values of operands as well as the results from evaluating subexpressions – see next point.

Since * and / have precedence over + and -, it would help to store operators in another stack. (Think of how you would evaluate a+b*c with operands/intermediate results on one stack and operators on the other.)

When you implement the evaluate method, you may want to test as you go, implementing code for and testing simple expressions, then building up to more complex expressions. The following is an example sequence of the kinds of expressions you may want to build with:

3 a 3+4 a+b 3+4*5 a+b*c

Then introduce parentheses

Then try nested parentheses

Then introduce array subscripts, but no parentheses

Then try nested subscripts, but no parentheses

Then try using parentheses as well as array subscripts

Then try mixing arrays within parentheses, parentheses within array subscripts, etc.




<strong>Correctness of expression and input files</strong>

All input expressions will be correctly formatted

All input files with values for variables and arrays will be correctly formatted, and will be guaranteed to have values for all variables in the expression that is being evaluated

So you don’t need to do any checking for correctness of inputs in any of the methods.

<h1>Running the evaluator</h1>

You can test your implementation by running the Evaluator driver on various expressions and input variable values file.

When creating your own variable values files for testing, make sure they are directly under the project folder, alongside etest1.txt and etest2.txt.

Since you are not going to turn in the Evaluator.java file, you may introduce debugging statements and other methods (such as printing out the variables or arrays array lists) as needed.

<strong>No variables</strong>

Enter the expression, or hit return to quit =&gt; 3

Enter variable values file name, or hit return if no variables =&gt;

Value of expression = 3.0




Enter the expression, or hit return to quit =&gt; 3-4*5

Enter variable values file name, or hit return if no variables =&gt;

Value of expression = -17.0




Enter the expression, or hit return to quit =&gt;

Neither of the expressions above have variables, so just hit return when asked for the variable values file name.

<strong>Variables, values loaded from file</strong>

Enter the expression, or hit return to quit =&gt; a

Enter variable values file name, or hit return if no variables =&gt; etest1.txt

Value of expression = 3.0




Enter the expression, or hit return to quit =&gt;

Since the expression has a variable, a, the evaluator needs to be supplied with a file that has a value for it. Here’s what etest1.txt looks like:

a 3   b 2

A 5 (2,3) (4,5)   B 3 (2,1)   d 56

Each line of the file begins with a variable name. For simple variables, the name is followed by the variable’s integer value. For arrays, the name is followed by the array’s length, which is followed by a series of (index,integer value) pairs.

Note: The index and integer value pairs must be written with no spaces around the index or integer value.

So, for instance, (2, 3) or ( 2,3) or (2 ,3) are all incorrect.

Make sure you adhere to this requirement when you create your own input files for testing.

If the value at a particular array index is not explicitly listed, it is set to 0 by default.

So, in the example above, A = [0,0,3,0,5] and B = [0,0,1]

Note that the variable values file can have values for any number of variables, so that it can be used as input for several expressions that contain one or more of the variables in the file.

Here are a couple more evaluations of expressions for which the variable values are loaded from etest1.txt:

Enter the expression, or hit return to quit =&gt; (a + A[a*2-b])

Enter variable values file name, or hit return if no variables =&gt; etest1.txt

Value of expression = 8.0




Enter the expression, or hit return to quit =&gt; a – (b+A[B[2]])*d + 3   Enter variable values file name, or hit return if no variables =&gt; etest1.txt

Value of expression = -106.0




Enter the expression, or hit return to quit =&gt;

For a change of pace, here’s etest2.txt, which has the following variables and values:

varx 6   vary 5   arrayA 10 (3,5) (8,12) (9,1)

And here are evaluations using this file:




Enter the expression, or hit return to quit =&gt; arrayA[arrayA[9]*(arrayA[3]+2)+1]-varx

Enter variable values file name, or hit return if no variables =&gt; etest2.txt

Value of expression = 6.0




Enter the expression, or hit return to quit =&gt;




<h1>Frequently Asked Questions</h1>

<strong>Q: Are array names all uppercase?</strong>

A: No. Arrays could have lower case letters in their names. You can tell if a variable is an array if it is followed by an opening square bracket. See, for example, the last example in the “Expression” section, in which varb and varz are arrays:

(varx + vary*varz[(vara+varb[(a+b)*33])])/55

<strong>Q: Can we delete spaces from the expression?</strong>

A: Sure.

<strong>Q: Will the expression contain negative numbers?</strong>

A: No. The expression will NOT have things like a*-3 or x+(-y). It will ONLY have the BINARY operators +, -, /, and *. In other words, each of these operators will need two values (operands) to work on. (The – in front of 3 in a*-3 is called a UNARY minus. UNARY operators will NOT appear in the input expression.)

However, it is possible that in the process of evaluating the expression, you come across negative values, either because they appear in the input file, or because they are the result of evaluation. For instance, when evaluating a+b, a=6 and b=-9 as input values, and a result of -3 is a perfectly legitimate scenario.

<strong>Q: What if an array index evaluates to a non-integer such as 5/2?</strong>

A: Truncate it and use the resulting integer as the index.

<strong>Q: Could an array index evaluate to a negative integer?</strong>

A: No, you will not be given any input expression or values that would result in a negative integer value for an array index. In other words, you will not need to account for this situation in your code.

<strong>Q: What should I do on divide by zero?</strong>

A: You don’t need to check for this situation.

<strong>Q: Could an array name be the same as a simple variable?</strong>

A: No. All variable names, for both simple variables and arrays, are unique.

<strong>Q: Should the expression “()” be reported as an error?</strong>

A: You don’t have to do any error checking on the legality of the expression in the makeVariableLists or evaluate methods. When these methods are called, you may assume that the expression is correctly constructed. Which means you will not encounter an expression without at least one constant or variable, and all parens and brackets will be correctly formatted.

<strong>Q: Can I convert the expression to postfix, then evaluate the postfix expression?</strong>

A: NO!!! You have to work with the given traditional/infix form of the expression.