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

The constructor of the most generic data structure takes in the following:

* ``ul`` - the coordinates of the upper-left corner of the boundary for the data structure
* ``ur`` - the coordinates of the upper-right corner of the boundary for the data structure
* ``ll`` - the coordinates of the lower-left corner of the boundary for the data structure
* ``lr`` - the coordinates of the lower-right corner of the boundary for the data structure
* ``aligned_edge`` - the edge towards which the data structure will be scaled if it grows out of the boundary (only applies if the data structure is dynamic in size)
* ``color`` - the color of the shapes visualised as part of the data structure *[Optional - defaults to* ``WHITE`` *]*
* ``text_color`` - the color of the text label visualised as part of the data structure *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - the weight of the text label visualised as part of the data structure *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - the font of the text label visualised as part of the data structure *[Optional - defaults to* ``"Times New Roman"`` *]*

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

Any data structure has the following inbuilt functions implemented:

``shrink(self, new_width, new_height)``
"""""""""""""""""""""""""""""""""""""""
Resizes the entire data structure by calculating a scale factor based on ``new_width`` and ``new_height`` provided.

In most cases, the scaling will be done directly, aligning to ``aligned_edge``; however, the function ``shrink2`` provides an alternative way of scaling the data structure in place and then moving it to align the ``aligned_edge``.

``will_cross_boundary(self, object_dim, boundary_name)``
""""""""""""""""""""""""""""""""""""""""""""""""""""""""
Checks if the given dimension ``object_dim`` will cross the boundary specified by ``boundary_name``. The check is done by calling the corresponding function ``will_cross_top_boundary``, ``will_cross_bottom_boundary``, ``will_cross_right_boundary`` or ``will_cross_left_boundary``.

``add(self, obj)``
""""""""""""""""""
Adds the given ``obj`` into the ``VGroup`` that holds all components of the data structure.

Abstract Methods
^^^^^^^^^^^^^^^^^^

The following abstract methods are to be implemented by any data structure class, as different data structures may have different implementation.

``create_init(self, ident)``
"""""""""""""""""""""""""""""
Creates an initial visualisation of the data structure with the label ``ident`` when it's instantiated.

``shrink_if_cross_boundary(self, obj)``
"""""""""""""""""""""""""""""""""""""""
Checks if the data structure is growing out of the boundary when ``obj`` is added and resizes the data structure if necessary.

``clean_up(self)``
""""""""""""""""""
Cleans up the current data structure visualisation, which is helpful when a data structure is no longer used. The most common way of doing this is to fade out the data structure visualisation using ``FadeOut``.


Stack
-----

Constructor
^^^^^^^^^^^

The constructor of Stack takes in the exact same arguments as ``Data Structure`` with the same default values.

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

``push(self, obj, creation_style=None)``
"""""""""""""""""""""""""""""""""""""""""
Animates the push operation of a new item ``obj``. The animation consists of visualising the creation of the ``obj`` using ``creation_style`` (optional and defaults to ``"FadeIn"``), as well as moving ``obj`` to the top of the stack.

``push_existing(self, obj)``
"""""""""""""""""""""""""""""
Animates a special form of push operation when the item to be pushed - ``obj`` - has been created already. The animation would use the existing ``obj`` and push it onto the stack.

``pop(self, obj, fade_out=True)``
"""""""""""""""""""""""""""""""""
Animates the pop operation. The animation consists of moving the ``obj`` off the stack and (optionally) fade out ``obj`` if it's no longer being used.


Array
------

Constructor
^^^^^^^^^^^

The constructor of Array takes in the following:

* ``values`` - list of values corresponding to each index of the array
* ``title`` - the text label to be displayed with the array
* ``boundaries`` - coordinates of boundary that the array has to stay within
* ``padding`` - specifies whether to add a padding between the title and the shape visualisation *[Optional - defaults to* ``True`` *]*
* ``color`` and ``text_color`` - same as for all data structures *[Optional -* ``color`` *defaults to* ``BLUE`` *and* ``text_color`` *defaults to* ``WHITE`` *]*

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

``build(self, coord=None)``
""""""""""""""""""""""""""""
Arranges each element of the array to be next to each other and adds in the title on the left of the array. The final ``Array`` object is then returned.

The optional argument ``coord`` specifies the left most coordinate of the array (defaults to where the title is), which is particularly useful when the array elements are updated.

``swap_mobjects(self, i1, i2)``
"""""""""""""""""""""""""""""""
Animates the normal "quick" ``swap`` method, which swaps the 2 elements at ``i1`` and ``i2`` directly.

``clone_and_swap(self, i1, i2)``
""""""""""""""""""""""""""""""""
Animates the special form of ``swap`` when ``longSwap`` is set to ``true``. This would create a visualisation of the temp variable (a clone) and its usage, which is often seen when swapping array elements programmatically.

``update_element(self, idx, v, color=None)``
""""""""""""""""""""""""""""""""""""""""""""
Animates updating the element at index ``idx`` with value ``v``. The optional argument ``color`` represents the new color of the text that corresponds to the specific element (defaults to ``None``, which is the original ``text_color``).

``update_array_elements(self)``
""""""""""""""""""""""""""""""""
Helper function for ``append`` that updates the array elements stored so far and recomputes the new dimension for the array (so that it fits within the boundary).

``append(self, v)``
"""""""""""""""""""
Since the ``List`` data structure has been added using the existing ``Array`` data structure, this function animates the ``append`` method supported by ``List``. This would visualise adding a new element with value ``v`` at the end of a resizable ``List``.


Array 2D
--------

Constructor
^^^^^^^^^^^

The constructor of 2D Array takes in the many of the same arguments as normal ``Array`` does, with the following differences:

* ``values`` - list of lists of values corresponding to each element of the array
* no ``padding`` argument required

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

``build(self, creation_style=None)``
""""""""""""""""""""""""""""""""""""
Animates the creation of a 2D Array with the optional ``creation_style`` (defaults to ``FadeIn``).

``replace_row(self, row_index, new_values)``
""""""""""""""""""""""""""""""""""""""""""""
Animates updating the row specified by ``row_index`` with the given values ``new_values``, which normally corresponds to a row assignment of a 2D Array.

``swap_mobjects(self, i1, j1, i2, j2)``
"""""""""""""""""""""""""""""""""""""""
Animates swapping 2 elements of the 2D Array specified by ``(i1, j1)`` and ``(i2, j2)``. The visualisation would first dim the rest of the 2D Array to indicate which elements are being swapped, before fading the rest of the array back to the original ``text_color``.


Tree
-----

Constructor
^^^^^^^^^^^

The constructor of Tree takes in the many of the same arguments as ``Data Structure`` with the same default values. The different ones are as follows:

* ``root`` - the root node of the tree
* ``identifier`` - text label for the tree
* ``radius`` - radius of the node of the tree *[Optional - defaults to* ``0.6`` *]*
* ``color`` - same as ``Data Structures`` but defaults to ``RED``
* ``text_color`` - same as ``Data Structures`` but defaults to ``BLUE``

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

``update_root(self, node)``
""""""""""""""""""""""""""""
Updates the root of the tree with ``node``.

``check_if_child_will_cross_boundary(self, parent, child, is_left)``
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
Checks whether adding ``child`` will make the tree with ``parent`` cross the boundary. The ``is_left`` flag indicates which side the ``child`` will be added.

``set_right(self, parent, child)``
"""""""""""""""""""""""""""""""""""
Animates setting ``child`` as the right child of ``parent``. Assumes that ``parent`` is in the tree. The check for scaling and the corresponding animations are also done by calling ``_resize_after_modification``.

``set_left(self, parent, child)``
"""""""""""""""""""""""""""""""""""
Animates setting ``child`` as the left child of ``parent``. Assumes that ``parent`` is in the tree. The check for scaling and the corresponding animations are also done by calling ``_resize_after_modification``.

``delete_right(self, parent)``
""""""""""""""""""""""""""""""
Animates removing the right child of ``parent``. Assumes that ``parent`` is in the tree. The check for scaling and the corresponding animations are also done by calling ``_resize_after_modification``.

``delete_left(self, parent)``
"""""""""""""""""""""""""""""
Animates removing the left child of ``parent``. Assumes that ``parent`` is in the tree. The check for scaling and the corresponding animations are also done by calling ``_resize_after_modification``.

``edit_node_value(self, node, text)``
""""""""""""""""""""""""""""""""""""""
Animates updating the value of ``node`` to ``text``.

``set_reference_right(self, parent, tree)``
"""""""""""""""""""""""""""""""""""""""""""
Animates setting the reference of the right child of ``parent`` to ``tree``. The check for scaling and the corresponding animations are also done by calling ``_resize_after_modification``.

``set_reference_left(self, parent, tree)``
"""""""""""""""""""""""""""""""""""""""""""
Animates setting the reference of the left child of ``parent`` to ``tree``. The check for scaling and the corresponding animations are also done by calling ``_resize_after_modification``.

``_resize_after_modification(self, animations)``
"""""""""""""""""""""""""""""""""""""""""""""""""
Check if scaling needs to be done and appends the animation that scales the tree to ``animations`` if needed. The check is done by calling ``check_positioning``.

``check_positioning(self)``
"""""""""""""""""""""""""""
Checks if the positioning and the size of the tree still fits within the boundary and fully utilises the space; scales the tree (bigger or smaller) if any of the check fails.

``crossing_bottom_border(self)``
"""""""""""""""""""""""""""""""""
Computes the scale factor when the tree crosses the bottom boundary.

``crossing_left_right_border(self, offset_x, scale=10e9)``
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
Computes the scle factor if tree crosses the left or right boundary with ``offset_x`` added on both sides.

``grow_if_small(self)``
"""""""""""""""""""""""
Scales the tree bigger if it is not utilising the space allocated fully.

``check_overlapping_children(self, node)``
""""""""""""""""""""""""""""""""""""""""""
Recursively checks if any of left and right child of ``node`` (or its children) are overlapping and scales the tree (or subtree) down if any nodes are overlapping.


Node
-----

The Node is the underlying representation of each node constructed as part of a ``Tree``. Therefore, these two classes are put in the same file `binary_tree.py <https://github.com/VAlgoLang/VAlgoLang/tree/master/src/main/resources/python/binary_tree.py>`_.

Constructor
^^^^^^^^^^^

The constructor of Node takes in all the arguments as ``Tree`` with the same default values. Additionally, it takes in the following:

* ``line_color`` - the color of the line connecting two nodes together *[Optional - defaults to* ``GREEN`` *]*
* ``highlight_color`` - the color to highlight the node outline in when the node has been accessed *[Optional - defaults to* ``YELLOW`` *]*

Inbuilt Functions
^^^^^^^^^^^^^^^^^^

``set_left(self, node, scale)``
"""""""""""""""""""""""""""""""
Sets the left child of the node to ``node`` by calling ``set_left_mobject``. ``scale`` represents the scale factor of how much the tree has been scaled (initially starts as ``1``).

``set_left_mobject(self, shape, vgroup, scale)``
""""""""""""""""""""""""""""""""""""""""""""""""
Animates setting the left of ``shape`` to ``vgroup`` - moving ``vgroup`` to lower left of ``shape`` and adding in the line that connects the two. ``scale`` is passed from ``set_left`` and used to obtain the position offset from ``shape``.

``set_right(self, node, scale)``
"""""""""""""""""""""""""""""""""
Sets the right child of the node to ``node`` by calling ``set_right_mobject``. ``scale`` represents the scale factor of how much the tree has been scaled (initially starts as ``1``).

``set_right_mobject(self, shape, vgroup, scale)``
"""""""""""""""""""""""""""""""""""""""""""""""""
Animates setting the right of ``shape`` to ``vgroup`` - moving ``vgroup`` to lower left of ``shape`` and adding in the line that connects the two. ``scale`` is passed from ``set_right`` and used to obtain the position offset from ``shape``.

``set_reference(self, tree, scale, left)``
""""""""""""""""""""""""""""""""""""""""""
Sets the left or right child of the node to be a reference to ``tree`` (in this case a text label) as data structures are passed by reference. The flag ``left`` indicates whether the left child or the right child is set. ``scale`` represents the scale factor of how much the tree has been scaled (initially starts as ``1``).

``edit_node_value(self, text)``
"""""""""""""""""""""""""""""""""
Changes the text representing the value of the node to ``text``.

``highlight(self, color)``
""""""""""""""""""""""""""""
Highlights the node outline to ``color``.

``unhighlight(self)``
"""""""""""""""""""""""
Unhighlights the node outline.

``set_radius(self, new_radius)``
""""""""""""""""""""""""""""""""""
Changes the radius of the node to ``new_radius`` and scales the node if needed.

``delete_left(self)``
"""""""""""""""""""""""
Animates deleting the left child of the node. Assumes that the node has a left child.

``delete_right(self)``
"""""""""""""""""""""""
Animates deleting the right child of the node. Assumes that the node has a right child.


Code Block
----------

The Code Block is your inputted VAlgoLang code which appears at the bottom left of your screen (by default).

The positioning and whether the Code Block should be rendered are controlled by the Stylesheet. Please refer to the :doc:`Customising Your Animation <customisation>` section for a more detailed description of how the Stylesheet works.

Constructor
^^^^^^^^^^^

The constructor of Code Block takes in the following:

* ``code`` - list of strings representing each line of code
* ``boundaries`` - coordinates of boundary that the code block has to stay within
* ``syntax_highlighting`` - flag indicating whether syntax highlighting of the code is turned on or not
* ``syntax_highlighting_style`` - the style of syntax highlighting *[Optional - defaults to* ``"inkpot"`` *]*
* ``text_color`` - color of the code *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - weight of the code *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - font of the code *[Optional - defaults to* ``"Times New Roman"`` *]*
* ``tab_spacing`` - size of tabulation within the code *[Optional - defaults to* ``2`` *]*

For the full list of possible syntax highlighting style, please refer to the :doc:`Customising Your Animation <customisation>` section.

Inbuilt Functions
^^^^^^^^^^^^^^^^^

``build(self)``
""""""""""""""""
Arranges the code block to be correctly formatted and returns the resultant ``VGroup``.

``get_line_at(self, line_number)``
""""""""""""""""""""""""""""""""""
Returns the ``Text`` of the line of code specified by ``line_number``.

Tracking the line that is currently executing is done with an ArrowTip and the ``move_arrow_to_line`` function. If you wish to change that shape, color, or scale, change this line in your construct function.

.. code :: python

    def construct(self):
        ...
        pointer = ArrowTip(color=YELLOW).scale(0.7).flip(TOP)


Variable Block
---------------

The Variable Block displays the list of most recently updated variables and their values at the top left of your screen (by default).

The positioning and whether the Variable Block should be rendered are controlled by the Stylesheet. Please refer to the :doc:`Customising Your Animation <customisation>` section for a more detailed description of how the Stylesheet works.

Constructor
^^^^^^^^^^^

The constructor of Variable Block takes in the following:

* ``variables`` - list of strings representing the variables and their values
* ``boundaries`` - coordinates of boundary that the variable block has to stay within
* ``text_color`` - color of the text *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - weight of the text *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - font of the text *[Optional - defaults to* ``"Times New Roman"`` *]*

Inbuilt Functions
^^^^^^^^^^^^^^^^^

``build(self)``
""""""""""""""""
Arranges the variable block to be correctly formatted and returns the resultant ``VGroup``.

``update_variable(self, variables)``
"""""""""""""""""""""""""""""""""""""
Animates updating the variable strings with the given argument ``variables``.


Subtitle Block
--------------

The Subtitle Block displays the list of most recently updated variables and their values at the top left of your screen (by default).

The Subtitle Block holds subtitles generated by the subtitle annotations and the positioning of the Subtitle Block is controlled by the Stlysheet. Please refer to the :ref:`Subtitles <subtitlesannotation>` and :doc:`Customising Your Animation <customisation>` sections for a more detailed description of how the subtitle annotations and Stylesheet works.

Constructor
^^^^^^^^^^^

The constructor of Variable Block takes in the following:

* ``end_time`` - time that the subtitle should disappear
* ``boundaries`` - coordinates of boundary that the subtitle block has to stay within
* ``text_color`` - color of the subtitle text *[Optional - defaults to* ``WHITE`` *]*
* ``text_weight`` - weight of the subtitle text *[Optional - defaults to* ``NORMAL`` *]*
* ``font`` - font of the subtitle text *[Optional - defaults to* ``"Times New Roman"`` *]*

Inbuilt Functions
^^^^^^^^^^^^^^^^^

``change_text(self, text)``
"""""""""""""""""""""""""""
Changes the subtitle text to ``text``.

``display(self, text, end_time)``
"""""""""""""""""""""""""""""""""
Displays the given ``text`` as subtitle until the specified ``end_time`` has passed.

``clear(self)``
""""""""""""""""
Clears the current subtitle.

``action(self)``
""""""""""""""""
Same as ``clear``.


Building Blocks
----------------
The visualisation of data structures is built on top of the following building blocks. Feel free to reuse them if you wish to add your own data structure visualisation!

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

To add an additional element, create it, and group it with the ``VGroup``.
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

To add an additional element, create it, and group it with the ``VGroup``.

Inbuilt Functions
"""""""""""""""""

``replace_text(self, new_text, color=None)``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Animates replacement of the text lablel to ``new_text`` inside the rectangle. The optional argument ``color`` represents to the new color of the text (defaults to the same as the original ``text_color``).

``clean_up(self)``
~~~~~~~~~~~~~~~~~~
Cleans up the current Rectangle Block visualisation.


Utility Functions
-----------------

The following is a list of all the utility functions implemented so far, which help to create repeated animation. Feel free to use them if you wish to generate your own animation or contribute!

* ``place_at(self, group, x, y)`` - places ``group`` at the coordinate specified by ``(x, y, 0)``.
* ``move_relative_to_edge(self, group, x, y)`` - moves ``group`` relative to the edge specified by ``(x, y, 0)``.
* ``move_relative_to_obj(self, group, target, x, y)`` - moves ``group`` relative to the object ``target`` specified by ``(x, y, 0)``.
* ``place_relative_to_obj(self, group, target, x, y)`` - places ``group`` relative to the object ``target`` with the offset specified by ``(x, y, 0)``.
* ``fade_out_if_needed(self, mobject)`` - fades out ``mobject`` if it is already on the Scene.
* ``play_animation(self, *args, run_time=1.0)`` - plays the animation(s) passed in as ``*args`` with optional ``run_time`` (defaults to ``1.0``). This is particularly useful as it accounts for all the ``time_object`` that have a duration of time they should appear for, such as ``Subtitle Block``.
* ``move_arrow_to_line(self, line_number, pointer, code_block, code_text)`` - moves the ``pointer`` next to the line of code specified by ``line_number``. Scrolling is also handled here if needed by calling the corresponding ``scroll_down`` and ``scroll_up`` functions. 

The following utility functions are inspired from https://www.reddit.com/r/manim/comments/bubyj2/scrolling_mobjects/

* ``scroll_down(self, group, scrolls)`` - scrolls the ``group`` (``code_text`` in the interpreter) down by ``scrolls`` number of times.
* ``scroll_up(self, group, scrolls)`` - scrolls the ``group`` (``code_text`` in the interpreter) up by ``scrolls`` number of times.