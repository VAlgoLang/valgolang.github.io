Exit Status
=====================================

When compiling ManimDSL the compiler can return a variety of informative status codes.

0: Success
-----------------

The 0 exit status code means that compilation was successful.

100: Syntax Error
-----------------

The 100 exit status code means there are one or more syntax errors in the file being compiled.

.. code :: none

    Errors detected during compilation 
    Exit code: 100
    Syntax error at 1:9: missing ';' at ''<EOF>'
    let a = 5

200: Semantic Error
--------------------

The 200 exit status code means there are one or more semantic errors in the file being compiled.

<- Insert Example ->