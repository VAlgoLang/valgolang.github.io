Python Library
=====================================

The interpreter uses manim to create animations for your code and the following prebuilt Python libraries define the standard visualisation for different data structures.
Although this is a fixed standard way of representing data structures, you are able to change the style attributes through the stylesheet or even modify our functions to represent data structures the way you want!

All of the utility functions can be found at `src/main/resources/python/util.py <https://github.com/VAlgoLang/VAlgoLang/tree/master/src/main/resources/python/util.py>`_, and all of the shapes/data structures are in their own class (i.e. RectangleBlock is in `src/main/resources/python/rectangle.py <https://github.com/VAlgoLang/VAlgoLang/tree/master/src/main/resources/python/rectangle.py>`_)

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


Stack
-----

Constructor
^^^^^^^^^^^

The constructor of Stack takes in the exact same argument as ``Data Structure``.

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

``push``
""""""""
Animates the push operation of a new item ``obj``. The animation consists of visualising the creation of the ``obj`` using ``creation_style`` (optional and defaults to ``"FadeIn"``), as well as moving ``obj`` to the top of the stack.

``push_existing``
""""""""""""""""""
Animates a special form of push operation when the item to be pushed - ``obj`` - has been created already. The animation would use the existing ``obj`` and push it onto the stack.

``pop``
"""""""
Animates the pop operation. The animation consists of moving the ``obj`` off the stack and (optionally) fade out ``obj`` if it's no longer being used.


Array
------

Constructor
^^^^^^^^^^^

The constructor of Array takes in the following:

* ``values`` - list of values corresponding to each index of the array
* ``title`` - the text label to be displayed with the array
* ``boundaries`` - coordinates of boundary
* ``padding`` - specifies whether to add a padding between the title and the shape visualisation
* ``color`` and ``text_color`` - same as for all data structures

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

``build``
"""""""""

``swap_mobjects``
""""""""""""""""""

``clone_and_swap``
""""""""""""""""""""

``update_element``
"""""""""""""""""""

``update_array_elements``
""""""""""""""""""""""""""

``append``
""""""""""


Code Block
----------

The Code Block is your inputed VAlgoLang code which appears at the bottom left of your screen (by default).

The positioning and whether the Code Block should be rendered are controlled by the Stlysheet. Please refer to the :doc:`Customising Your Animation <customisation>` section for a more detailed description of how the Stylesheet works.

Constructor
^^^^^^^^^^^

The constructor of Code Block takes in the following:

* ``code`` - list of strings representing each line of code
* ``boundaries`` - coordinates of boundary
* ``syntax_highlighting`` - flag indicating whether syntax highlighting of the code is turned on or not
* ``syntax_highlighting_style`` - the style of syntax highlighting *[Optional - defaults to* ``"inkpot"`` *]*
* ``text_color`` - color of the code *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - weight of the code *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - font of the code *[Optional - defaults to* ``"Times New Roman"`` *]*
* ``tab_spacing`` - size of tabulation within the code *[Optional - defaults to* ``2`` *]*

For the full list of possible syntax highlighting style, please refer to the :doc:`Customising Your Animation <customisation>` section.

Inbuilt Functions
^^^^^^^^^^^^^^^^^

``build``
""""""""""
Arranges the code block to be correctly formatted and returns the resultant ``VGroup``.

``get_line_at``
""""""""""""""""
Returns the ``Text`` of the line of code specified by ``line_number``.

Tracking the line that is currently executing is done with an ArrowTip and the ``move_arrow_to_line`` function. If you wish to change that shape, color, or scale, change this line in your construct function.

.. code :: python

    def construct(self):
        ...
        pointer = ArrowTip(color=YELLOW).scale(0.7).flip(TOP)


Building Blocks
----------------
The visualisation of data structures are built on top of the following building blocks. Feel free to reuse them if you wish to add your own data structure visualisation!

Initial Structure
^^^^^^^^^^^^^^^^^
An initial structure represents the empty state for a data structure, such as for a ``Stack``.

It consists of a line, which can be horizontal or vertical, and a text label indicating the variable name under the line.

Constructor
"""""""""""

The constructor of Initial Structure takes in the following:

* ``text`` - text that is labelled under the line
* ``angle`` - angle of rotation (``0`` for horizontal line, ``TAU/4`` for vertical line)
* ``length`` - length for the line *[Optional - defaults to* ``1.5`` *]*
* ``color`` - color of the line *[Optional - defaults to* ``WHITE`` *]*
* ``text_color`` - color of the text label *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - weight of the text label *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - font of the text label *[Optional - defaults to* ``"Times New Roman"`` *]*

To add an additional element, create it, and group it with the VGroup.
To change the default position of the label and the distance between the label and the line, change ``DOWN`` and ``SMALL_BUFF`` respectively.

Rectangle Block
^^^^^^^^^^^^^^^

A Rectangle Block represents a rectangle shape with text inside it.

Constructor
"""""""""""

The constructor of Rectangle Block takes in the following:

* ``text`` - text placed inside the rectangle
* ``target`` - a target that the rectangle block would be scaled to match *[Optional - defaults to* ``None`` *]*
* ``width`` - width of the rectangle *[Optional - defaults to* ``1.5`` *]*
* ``width`` - height of the rectangle *[Optional - defaults to* ``0.75`` *]*
* ``color`` - color of the rectangle outline *[Optional - defaults to* ``BLUE`` *]*
* ``text_color`` - color of the text inside the rectangle *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - weight of the text inside the rectangle *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - font of the text inside the rectangle *[Optional - defaults to* ``"Times New Roman"`` *]*

To add an additional element, create it, and group it with the VGroup.

Inbuilt Functions
"""""""""""""""""

``replace_text``
~~~~~~~~~~~~~~~~
Animates replacement of the text lablel to ``new_text`` inside the rectangle.

``clean_up``
~~~~~~~~~~~~~
Cleans up the current Rectangle Block visualisation.
