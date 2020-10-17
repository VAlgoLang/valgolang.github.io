Usage
===========

The Compiler has some command line options:

.. code:: bash

    Usage: manimdsl [-hpV] [-o=<output>] [-q=<quality>] <file>
    ManimDSL compiler to produce manim animations
          <file>                The manimdsl file to compile and animate
      -h, --help                Show this help message and exit.
      -o, --output=<output>     The animated mp4 file location (default: out.mp4)
      -p, --python              Output generated python & manim code (optional)
      -q, --quality=<quality>   Quality of animation. [low, high] (default: low)
      -V, --version             Print version information and exit.


Command Line Arguments
----------------------

<file>
~~~~~~~~~~~~~~~~~~~~~

 - The ``.manimdsl`` file to compile

-o=<output>, --output=<output>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - The path to where the MP4 file should be saved (defaults to ``out.mp4``)
 - If the path does not exist, all the subdirectories will be created

-p, --python
~~~~~~~~~~~~~~~~~~~~~

 - Flag to output the Manim and Python generated code
 - The Python file will be saved with the same name as the output MP4 file (and so is defaulted to ``out.py``)

-q=<quality>, --quality=<quality>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - Quality of the generated animation (default: low)
 - Available options: ``high`` and ``low``

-h, --help
~~~~~~~~~~~~~~~~~~~~~

 - Produce the help message shown above