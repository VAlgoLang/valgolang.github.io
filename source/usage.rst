Usage
===========

The Compiler has some command line options:

.. code:: bash

    Usage: manimdsl [-hpV] [-o=<output>] [-q=<quality>] <file>
    ManimDSL compiler to produce manim animations
          <file>                The manimdsl file to compile and animate.
      -f, --show_file_in_finder Show the output file in finder.
      -h, --help                Show this help message and exit.
      -m, --manim               Only output generated python & manim code.
      -o, --output=<output>     The animated mp4 file location (default: out.mp4).
      -p, --python              Output generated python & manim code (optional).
          --preview             Automatically open the saved file once its done.
      -q, --quality=<quality>   Quality of animation. [low, high] (default: low).
      -V, --version             Print version information and exit.


Command Line Arguments
----------------------

<file>
~~~~~~~~~~~~~~~~~~~~~

 - The ``.manimdsl`` file to compile

-f, --show_file_in_finder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - Flag to show the output file in finder automatically
 - The Python file will be saved with the same name as the output MP4 file (and so is defaulted to ``out.py``)

-m, --manim
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - Flag to only output generated python & manim code, and not create the animation
 - The path defaults to ``out.mp4`` in the same directory the compiler is called. Use -o (description below) to specifiy the path.

-o=<output>, --output=<output>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - The path to where the MP4 file should be saved (defaults to ``out.mp4`` in the same directory the compiler is called)
 - All the subdirectories specified in the path will be created

-p, --python
~~~~~~~~~~~~~~~~~~~~~

 - Flag to output the Manim and Python generated code
 - The Python file will be saved with the same name as the output MP4 file (and so is defaulted to ``out.py``)

--preview
~~~~~~~~~~~~~~~~~~~~~

 - Flag to open the generated animation automatically

-q=<quality>, --quality=<quality>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - Quality of the generated animation (default: low)
 - Available options: ``high`` and ``low``

-h, --help
~~~~~~~~~~~~~~~~~~~~~

 - Produce the help message shown above