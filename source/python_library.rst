Python Library
=====================================

The compiler uses manim to create animations for your code.
Although the compiler has a standard way of representing datastructures, you are able to modify our functions to represent them the way you want!

All of the utility functions can be found at `pythonLib/util.py <https://github.com/ManimDSL/ManimDSLCompiler/tree/master/pythonLib/util.py>`_, and all the shapes are in their own class (i.e. Rectangle_block is in `pythonLib/rectangle.py <https://github.com/ManimDSL/ManimDSLCompiler/tree/master/pythonLib/rectangle.py>`_)

Rectangles
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

Text Boxes takes in:
    - A text
    - A color for the text

If you want to change the way it appears on the screen, you will need to change that in your construct function.

.. code :: python

    def construct(self):
        ...
        text = Text_block("hello", BLUE).build()
        self.play(Write(assignment1))

Here, Write could be FadeIn, Flash, FadeToColor...

3: Code Block
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
