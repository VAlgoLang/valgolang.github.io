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

For equality we have two binary operators: equals ``==``, not equals ``!=``. 

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

**Logical Operators**

These have been implemented with the following binary operators: logical and ``&&``, logical or ``||`` and the unary not operator ``!``.

.. code :: javascript

    let x = true;
    let y = x && false; // y = false
    let z = x || y;     // z = true
    let y = !x;         // y = false


*Precedence*

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

The if-then and if-then-else Statements
#############################################

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

In the above example first the ``x < 4`` condition will evaluate to false, then the ``x < 8`` condition evaluates to false and finally the ``x < 12`` condition evaluates to true. The program
will then execute the section of code corresponding to the second ``else-if`` and ``y`` will evaluate to 15.

Loops
###############

Loops in ManimDSL work much the same as they do in other programming languages. ManimDSL has two types of loops: for loops and while loops. They are best demonstrated using the following examples.

For loops
~~~~~~~~~

.. code :: javascript

    let array = Array<number>(){4, 2, 1, 3};
    let n = array.size();

    for i in range(n) {
        if (i == 2) {
            continue;
        }
        for j in range(n - 1 - i) {
            if (array[j] > array[j + 1]) {
                array.swap(j, j + 1);
            }
        }
    }

The ``range`` keyword specifies the index value sequence that the loop iterates over. Similar to Python, ``range`` in ManimDSL takes at most 3 arguments:

* ``start`` - (inclusive) start index value *[Optional - default is* ``0`` *]*
* ``end`` - (exclusive) end index value
* ``step`` - numeric difference between each number/character in the range sequence *[Optional - default is* ``1`` *]*


While loops
~~~~~~~~~~~~

.. code :: javascript

    let stack1 = Stack<number>(){1, 2, 3, 4, 5};
    let stack2 = Stack<number>();
    let i = 0;

    while (i < 3) {
        if (i == 1) {
            stack2.pop();
            break;
        }
        stack2.push(stack1.pop());
        i = i + 1;
    }

Within for loops and while loops, you can use the ``break`` keyword to terminate the loop at that point and resume execution after the loop, or the ``continue`` keyword to run the next iteration of the loop immediately.


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

Customisations to things such as colours, fonts and other attributes can be made through an external stylesheet described :ref:`over here <stylesheet>`.

Sleep
^^^^^^^^^^^^

The sleep command allows you to pause the animation at any code line for as many seconds as you would like. If you are constructing an online lecture this can give you some time to do a voice over.

.. code:: javascript
    
    ...
    sleep(2.5); // pauses the animation for 2.5 seconds before stepping onto the next line
    ...

.. _code_tracking:

Code Tracking
^^^^^^^^^^^^^^

On a statement level you can choose during code tracking to animate stepping into statements or stepping over them using the ``stepInto`` and ``stepOver`` blocks.

.. code:: javascript
    
    ...
    stepInto {
    let x = f(y);       // This will animate the execution of statements inside the function
    }

    stepOver {
    let z = f(y);       // This will simply step over the statement
    }
    ...


Structuring your program
-----------------------------

``Work in progress!``


Types
------------------------------

There are only two "kinds" of types in this language at the moment. 

* Primitives, such as ``boolean``, ``char`` and ``number``.
* Data structures, such as ``Stack<number>``. Data structures may define restrictions on the type parameters they permit.

.. _primitive_types:

Primitive Types
^^^^^^^^^^^^^^^

number
###############

A number is an arbitrary representation of a numeric value that in our transpiler is represented using Double precision.

.. code:: javascript

    let x: number = 5;
    let y: number = 4.5;

char
###############

Represents a 16-bit Unicode character.

.. code:: javascript

    let x: char = 'a';
    let y: char = '+';

boolean
###############

Represents boolean values true or false.

.. code:: javascript

    let x: boolean = true;
    let y: boolean = false;


Conversion Functions
####################

``toChar``
~~~~~~~~~~

*Arguments:* ``value: number | char``; *Return type:* ``char``

This method converts a ``number`` to its ASCII ``char`` value. It acts as an identity function when a ``char`` is given as input. 
The number is rounded to the nearest integer to perform the conversion.

.. code:: javascript

    toChar(97); // will return 'a'

``toNumber``
~~~~~~~~~~~~

*Arguments:* ``value: number | char``; *Return type:* ``number``

This method converts a ``char`` to its ASCII code value. It acts as an identity function when a ``number`` is given as input. 

.. code:: javascript

    toNumber('a'); // will return 97

.. _data_structures:

Data Structures
^^^^^^^^^^^^^^^

A rule of thumb is that data structures are the types of things you might have learnt in a CS class (trees, lists, and so on) and which you might find interesting to animate.
All primitives begin with a lower case letter while data structures will begin with a capitalised letter.

For those of you interested in the nuts and bolts, this distinction was made to make it clear in the type system for the programmer what sorts of variables should be centre-stage in the animation.
When combined with hiding data structures a string representation can appear in the variable state if desired alongside primitive values.

A comprehensive list of data structures "baked in" to the language is detailed below.

Stack<T>
###############

This has the following inbuilt methods:

``push``
~~~~~~~~~

*Arguments:* ``item: T``; *Return type:* ``void``

Pushes an item onto the top of the stack.

``pop``
~~~~~~~~~

*Arguments:* None; *Return type:* ``T``

Pops off the top element of the stack and returns this value.

``peek``
~~~~~~~~~

*Arguments:* None; *Return type:* ``T``

Returns the element on top of the stack without removing it.

``size``
~~~~~~~~~

*Arguments:* None; *Return type:* ``number``

Returns the current size of the stack.

``isEmpty``
~~~~~~~~~~~~~~

*Arguments:* None; *Return type:* ``boolean``

Returns ``true`` if the stack is currently empty.


Array<T>
###############

This has the following inbuilt methods:


``swap``
~~~~~~~~~

*Arguments:* ``index1: number``, ``index2: number``, (optional) ``longSwap: boolean``; *Return type:* ``void``

Swaps the elements at ``index1`` and ``index2`` in the array. The optional ``longSwap`` argument can be set to ``true`` in order to make the animation slightly longer, with a visualisation of the ``temp`` variable often seen when swapping array elements programmatically. The default value is ``false``, resulting in a 'quick swap'.


``size``
~~~~~~~~~

*Arguments:* None; *Return type:* ``number``

Returns the fixed size of the array.

Tree<T>
###############

The tree type encapsulates an underlying Node<T> object. The distinction between the Node and Tree types exist to allow you to be able to specify exactly which nodes in a subtree should be animated.
To animate a Node simply construct a Tree from it as defined below.

This has the following inbuilt methods:

``constructor``
~~~~~~~~~~~~~~~

*Arguments:* ``root: Node<T>?``; 

Constructs a Tree from a Root node, marking the node and all current and future children to be able to be animated as a data structure.

``root``
~~~~~~~~~

*Arguments:* None; *Return type:* ``Node<T>?``

Accesses underlying Root node of tree.

Node<T>
###############

This has the following inbuilt methods:

``constructor``
~~~~~~~~~~~~~~~

*Arguments:* ``root: T``; 

Constructs a Node from the value it will contain.

``left``
~~~~~~~~~

*Arguments:* None; *Return type:* ``Node<T>?``

Accesses left subtree. Returns null if no left subtree.

``right``
~~~~~~~~~

*Arguments:* None; *Return type:* ``Node<T>?``

Accesses right subtree. Returns null if no right subtree.

``value``
~~~~~~~~~

*Arguments:* None; *Return type:* ``T``

Extracts the value from the node.


Examples
############


To make this more concrete, note how the ``Stack<number>`` in the following animation is the focus of the attention as it is the primary data structure being used.


.. raw:: html

        <video src="_static/intro.mp4" frameborder="0" allowfullscreen style=" width: 80%; height: 80%;" controls></video> 

