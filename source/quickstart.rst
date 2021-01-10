Quick Start
=============

Introduction
-----------------

Welcome to VAlgoLang's documentation!

VAlgoLang is a domain specific language that helps educators create animations for teaching students about data structures
and algorithms.

Here's a short example:

.. code:: javascript

    let stack = Stack<number>();
    stack.push(5);
    let x: number = stack.pop();

This would produce the video:

.. raw:: html

        <video src="_static/intro.mp4" frameborder="0" allowfullscreen style=" width: 80%; height: 80%;" controls></video>



Quick Start Guide
-------------------

The quickest way to get started with VAlgoLang is to head over to the **web interface** at `https://valgolang.netlify.app/ <https://valgolang.netlify.app/>`_. Take a look at the examples pane on the left hand side to get an idea of what you can do with the language and just get stuck in!

Alternatively, if you'd prefer to work locally, follow `these instructions <https://github.com/ManimDSL/ManimDSLCompiler#installation>`_ to install the required dependencies on your machine.

The next steps are to:

#. Take a look through our :doc:`language tour <tutorial>` to familiarise yourself with the syntax of VAlgoLang. It should be pretty easy to pick up if you have even a bit of programming experience!
#. Check out the :doc:`Customising Your Animation <customisation>` section for ideas on how to change the style attributes of your animation using the stylesheet. 

We hope you enjoy using VAlgoLang! Feel free to reach out to us on `GitHub <https://github.com/ManimDSL>`_ :)