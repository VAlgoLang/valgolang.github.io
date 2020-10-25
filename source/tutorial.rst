Language Tour
=====================================

ManimDSL is a statically typed language designed to leverage the Manim visualisation library to enable educators to succinctly express and visualise algorithms. The core language is small by design.

This tour will take you through some of the basic constructs of the language, many of which will be familiar to those with any programming background.
It is assumed you have at least very basic knowledge of programming in any other language (such as Python, JavaScript or Java). 


Note that this is an open source project and we welcome suggestions and improvements! If you would like to make a contribution feel free to submit a pull request `here <https://github.com/ManimDSL/ManimDSLCompiler/tree/master/>`_.


The Basics
----------

Variables
^^^^^^^^^^^^

Declaring and assigning a variable looks a lot like it does in any other language. 

Note that depending on your code style during declaration you may choose to omit or specify the type of the variable.

.. code :: javascript
    
    let x = 4;
    let y: number = 4;
    let x: boolean = false; 


Arithmetic Expressions
^^^^^^^^^^^^^^^^^^^^^^

Arithmetic expressions also look a lot like in any other programming language (for good reason!). 

.. code :: javascript
    
    let x = 4.5;
    x = (x * 2) + 3; // x = 12


Boolean Expressions
^^^^^^^^^^^^^^^^^^^
Boolean expressions for many are quite familiar, as we have taken inspiration from other programming languages.

**Equality**

We have for equality two binary operators: equals ``==``, not equals ``!=``. 

.. code :: javascript

    let x = 5;
    let y = x == 5; // y = true
    let z = x != 6; // z = true

**Comparison**

For comparison we have the following binary operators: less than ``<``, greater than ``>``, less than or equal ``<=`` and greater than or equal ``>=``.

.. code :: javascript
    
    let x = 5;
    let y = x < 3;  // y = false
    let z = x > 4;  // z = true
    let a = x <= 5; // a = true
    let b = x >= 6; // b = false

**Logical And and Or**

These have been implemented with the following binary operators: logical and ``&&``, logical or ``||``.

.. code :: javascript

    let x = true;
    let y = x && false; // y = false
    let z = x || y;     // z = true

**Logical Not**

This is implemented as the standard ``!`` unary operator.

..  code :: javascript

    let x = true;
    let y = !x;  // y = false


**Precedence**

The precedence for the boolean logical operators is as follows:

=========  ============ 
Operator    Precedence
---------  ------------
  ``!``        High 
  ``&&``       Medium
  ``||``       Low 
=========  ============

Examples

===================== ========= ==========================
 ``A || B && C``        means     ``A || (B && C)``
``A && B || C && D``    means    ``(A && B) || (C && D)``
``A && B && C || D``    means    ``((A && B) && C) || D``
``!A && B || C``        means    ``((!A) && B) || C``
===================== ========= ==========================

Constructors
^^^^^^^^^^^^

Data structures baked into the language have constructors. These can be invoked using the ``new`` keyword.

Note that if a data structure (as below) takes generic type arguments in their constructor they must not be omitted.

.. code :: javascript
    
    let stack = new Stack<number>;


Control structures
^^^^^^^^^^^^^^^^^^

**The if-then and if-then-else Statements**

The ``if-then`` statement is the most basic of all control flow statements. It tells your program to execute a section of code **only if** a condition evaluates
to true. Otherwise the program will jump to the end of the ``if-then`` statement. For example:

.. code :: javascript

    let x = 3;

    if(x < 5) {
        x = 5;
    }

    let y = x;

In the above example the condition ``x < 5`` is true as 3 is less than 5. So the program will execute the section of code inside the ``if-then`` and y will evaluate to 5.

The ``if-then-else`` statement provides another path of execution when the ``if-then`` condition evaluates to false. For example:

.. code :: javascript

    let x = 6;

    if(x < 5) {
        x = 5;
    } else {
        x = 10;
    }

    let y = x;

In the above example the ``if-then`` condition evaluates to false as 6 is greater than 5. So the program will execute the section of code inside the ``else`` block.

We can extend this even further by introducing ``else-if`` conditions where we can chain ``if-then-else`` statements together. This has the effect of going through the 
conditions in order and upon reaching the first condition that evaluates to true, that section of code is executed and then the program will jump to the end of the whole statement.
For example.

.. code :: javascript

    let x = 10;

    if(x < 4) {
        x = 5;
    } else if(x < 8) {
        x = 10;
    } else if(x < 12) {
        x = 15;
    } else {
        x = 20;
    }

    let y = x;

In the above example first the ``x < 4`` condition will be evaluated to false, then the ``x < 8`` which is also false and then the ``x < 12`` which evaluates to true. The program
will then execute the section of code corresponding to the second ``else-if`` and ``y`` will evaluate to 15.

Functions
^^^^^^^^^^^^

In order to compile a program with functions, please define all the functions at the top of the file before the statements.

The ways to define functions and make function calls are similar as they are in other languages.

Note that the return type must be defined if you intend to return anything from the function. If the return type is not specified, the function is assumed to be of type ``void``, so no ``return`` statement is allowed inside the function.

Also note that the arguments passed into any function are passed by reference, meaning that the changes made to the parameters inside the function will affect the original variables passed in.

.. code :: kotlin
    
    fun func1(number x): number {
        return x + 1;
    }

    fun func2(Stack<number> stack) {  // function assumed to be void as no return type is specified
        stack.push(5);
    }
.. code :: javascript

    let x : number = func1(5);

Controlling your animation
-----------------------------

To make dynamic changes to the end animation, you can insert special commands which won't show up in the code visualisation.

Customisations to things such as colours, fonts and other attributes can be made through an external stylesheet described `over here <#>`_.

Sleep
^^^^^^^^^^^^

The sleep command allows you to pause the animation at any code line for as many seconds as you would like. If you are constructing an online lecture this can give you some time to do a voice over.

.. code:: javascript
    
    ...
    sleep(2.5); // pauses the animation for 2.5 seconds before stepping onto the next line
    ...


Structuring your program
-----------------------------

``Work in progress!``


Data Structures and Primitives
------------------------------

There are only two "kinds" of types in this language at the moment. 

* Primitives, such as ``number``.
* Data structures, such as ``Stack<number>``. Data structures may define restrictions on the type parameters they permit.

A rule of thumb is that data structures are the types of things you might have learnt in a CS class (trees, lists, and so on) and which you might find interesting to animate.
All primitives begin with a lower case letter while data structures will begin with a capitalised letter.

A comprehensive list of data structures "baked in" to the language is as follows:

1) ``Stack<T>``

For those of you interested in the nuts and bolts, this distinction was made to make it clear in the type system what sorts of variables should be centre-stage in the animation.

To make this more concrete, note how the ``Stack<number>`` in the following animation is the focus of the attention as it is the primary data structure being used.


.. raw:: html

        <video src="_static/intro.mp4" frameborder="0" allowfullscreen style=" width: 80%; height: 80%;" controls></video> 

