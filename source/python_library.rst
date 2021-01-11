Python Library
=====================================

The interpreter uses manim to create animations for your code and the following prebuilt Python libraries define the standard visualisation for different data structures.
Although this is a fixed standard way of representing data structures, you are able to change the style attributes through the stylesheet or even modify our functions to represent data structures the way you want!

All of the utility functions can be found at `src/main/resources/python/util.py <https://github.com/ManimDSL/ManimDSLCompiler/tree/master/src/main/resources/python/util.py>`_, and all of the shapes/data structures are in their own class (i.e. Rectangle_block is in `src/main/resources/python/rectangle.py <https://github.com/ManimDSL/ManimDSLCompiler/tree/master/src/main/resources/python/rectangle.py>`_)

Data Structure
-----------------

This is the abstract base class that defines the common fields and functions shared across all the data structures.

Constructor
^^^^^^^^^^^

The constructor of the most generic data structure takes the following arguments:

* ``ul`` - the coordinates of the upper-left corner of the boundary for the data structure
* ``ur`` - the coordinates of the upper-right corner of the boundary for the data structure
* ``ll`` - the coordinates of the lower-left corner of the boundary for the data structure
* ``lr`` - the coordinates of the lower-right corner of the boundary for the data structure
* ``aligned_edge`` - the edge towards which the data structure will be scaled if it grows out of the boundary (only applies if data structure is dynamic)
* ``color`` - the color of the shapes visualised as part of the data structure *[Optional - defaults to* ``WHITE`` *]*
* ``text_color`` - the color of the text visualised as part of the data structure *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - the weight of the text visualised as part of the data structure *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - the font of the text visualised as part of the data structure *[Optional - defaults to* ``"Times New Roman"`` *]*

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

Any data structure has the following inbuilt functions implemented:

``shrink``
""""""""""
Resizes the entire data structure by calculating a scale factor based on ``new_width`` and ``new_height`` provided.

In most cases, the scaling will be done directly, aligning to ``aligned_edge``; however, the function ``shrink2`` provides an alternative way of scaling the data structure in place and then moving it to align the ``aligned_edge``.

``will_cross_boundary``
"""""""""""""""""""""""

Checks if the given dimension ``object_dim`` will cross the boundary spceified by ``boundary_name``. The check is done by calling the corresponding function ``will_cross_top_boundary``, ``will_cross_bottom_boundary``, ``will_cross_right_boundary`` or ``will_cross_left_boundary``.

``add``
"""""""

Adds the given ``obj`` into the ``VGroup`` that holds all components of the data structure.

Abstract Methods
^^^^^^^^^^^^^^^^^^

The following abstract methods are to be implemented by any data structure class, as different data structures may have different implementation.

``create_init``
"""""""""""""""

Creates an initial visualisation of the data structure when it's instantiated.

``shrink_if_cross_border``
""""""""""""""""""""""""""

Checks if the data structure is growing out of the boundary and resizes the data structure if necessary.

``clean_up``
"""""""""""""

Cleans up the current data structure visualisation, which is helpful when a data structure is no longer used.

Initial Structure
-----------------

An initial structure represents the empty state for any data structure.

It consists of a line, which can be horizontal or vertical, and a text label indicating the variable name under the line.

An Initial Structure takes in:
    - A text that is labelled under the line
    - An angle of rotation (``0`` for horizontal line, ``TAU/4`` for vertical line)
    - A length for the line *[Optional - default is* ``1.5`` *]*
    - A color for the line and text label *[Optional - default is* ``WHITE`` *]*

The Line Mobject with length (given or default) rotated by the given angle, and a TextMobject with the label, are grouped under a VGroup.
To add an additional element, create it, and group it with the VGroup.
To change the default position of the label and the distance between the label and the line, change ``DOWN`` and ``SMALL_BUFF`` respectively.

.. code :: python

    def build(self):
        line = Line(color=self.color)
        line.set_length(self.length)
        line.set_angle(self.angle)
        label = TextMobject(self.ident, color=self.color)
        label.next_to(line, DOWN, SMALL_BUFF)
        group = VGroup(label, line)
        return group

Rectangle
-----------------

Rectangles take in:
    - A text which is placed inside the rectangle
    - A width and height to for the rectangle dimensions
    - A color for the rectangle outline

A TextMobject with the text, and a Rectangle, are grouped under a VGroup.
To add an additional element, create it, and group it with the VGroup.

.. code :: python

    def build(self):
        inside_text = TextMobject(self.text)
        rectangle   = Rectangle(height=self.height, width=self.width, color=self.color)
        group       = VGroup(inside_text, rectangle)
        return group

Text Box
--------------------

Text Boxes take in:
    - A text
    - A color for the text

If you want to change the way it appears on the screen, you will need to change that in your construct function.

.. code :: python

    def construct(self):
        ...
        text = Text_block("hello", BLUE).build()
        self.play(Write(assignment1))

Here, Write could be FadeIn, Flash, FadeToColor...

Code Block
--------------------

The Code Block is your inputed ManimDSL code which appears at the bottom left of your screen.
If you do not want this code to appear, remove this part from the construct function.

.. code :: python

    def construct(self):
        # Remove all below lines
        code_block = Code_block(self.code)
        code_text = code_block.build()
        self.place_at(code_text, -1, 0)
        self.play(FadeIn(code_text))

Tracking the line that is currently executing is done with an ArrowTip. If you wish to change that shape, color, or scale, change this line in your construct function.

.. code :: python

    def construct(self):
        ...
        pointer = ArrowTip(color=YELLOW).scale(0.7).flip(TOP)

The ``move_arrow_to_line`` function is used to move the arrow to a specific line number. To change the moment at which you change the line number, you can move this line.
