Usage
===========

The Compiler has some command line options:

.. code:: bash

    Usage: manimdsl [-hpV] [-o=<output>] [-q=<quality>] <file>
    ManimDSL compiler to produce manim animations
          <file>                The manimdsl file to compile and animate.
      -f, --open_file           Show the output file in file manager (optional).
      -h, --help                Show this help message and exit.
      -m, --manim               Only output generated python & manim code (optional).
      -o, --output=<output>     The animated mp4 file location (default: out.mp4).
      -p, --python              Output generated python & manim code (optional).
          --preview             Automatically open the saved file once its done (optional).
      -q, --quality=<quality>   Quality of animation. [low, high] (default: low).
      -V, --version             Print version information and exit.


Command Line Arguments
----------------------

<file>
^^^^^^^^^^^^

 - The ``.manimdsl`` file to compile

-f, --open_file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - Flag to show the output file in file manager

-m, --manim
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - Flag to only output generated python & manim code, and not create the animation
 - The path defaults to ``out.py`` in the same directory the compiler is called. Use -o (description below) to specifiy the path

-o=<output>, --output=<output>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 - The path to where the MP4 file should be saved (defaults to ``out.mp4`` in the same directory the compiler is called)
 - All the subdirectories specified in the path will be created

-p, --python
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 - Flag to output the Manim and Python generated code
 - The Python file will be saved with the same name as the output MP4 file (and so is defaulted to ``out.py``)

--preview
~~~~~~~~~~~~~~~~~~~~~

 - Flag to open the generated animation automatically

-q=<quality>, --quality=<quality>
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 - Quality of the generated animation (default: low)
 - Available options: ``high`` and ``low``

-h, --help
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

 - Produce the help message shown above
 
 
Program Exit Status
-------------------

When compiling ManimDSL the compiler can return a variety of informative status codes.

0: Success
^^^^^^^^^^

The 0 exit status code means that compilation was successful.

100: Syntax Error
^^^^^^^^^^^^^^^^^

The 100 exit status code means there are one or more syntax errors in the file being compiled.

.. code :: none

    Errors detected during compilation 
    Exit code: 100
    Syntax error at 1:9: missing ';' at ''<EOF>'
    let a = 5

200: Semantic Error
^^^^^^^^^^^^^^^^^^^

The 200 exit status code means there are one or more semantic errors in the file being compiled.

An invalid declaration like below will lead to a semantic error.

.. code :: none

    let x: number = new Stack;

.. code :: none

    Errors detected during compilation 
    Exit code: 200
    Semantic error at 1:0: Cannot assign expression of type Stack<number> to x, which is of type number
    
300: Runtime Error
^^^^^^^^^^^^^^^^^^^

The 300 exit status code means there was an error during the excution of the program.

For instance "popping" from an empty stack will cause a Runtime Error.

.. code :: none

    let x = new Stack<number>;
    x.pop();

.. code :: none

    Error detected during program execution. Animation could not be generated. 
    Exit code: 300
    Your program failed at line 2: Attempted to pop from empty stack x
