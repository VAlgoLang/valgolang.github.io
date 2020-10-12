Python Library
=====================================

We are using manim to create animations for your code. 
Although we have a standard way of representing datastructures, you are able to modify our functions to represent them the way you want!

All of our utility functions can be found at ```pythonLib/util.py`` <https://github.com/ManimDSL/ManimDSLCompiler/tree/master/pythonLib/util.py>`_, and all of our shapes are in their own class (i.e. Rectangle_block is in ```pythonLib/util.py`` <https://github.com/ManimDSL/ManimDSLCompiler/tree/master/pythonLib/rectangle.py>`_)

Rectangles
-----------------

Our Rectangles take in:
    - A text which is placed inside the rectangle 
    - A width and height to for the rectangle dimensions
    - A color for the rectangle outline

We create a TextMobject with the text, and a Rectangle, and group these two under a VGroup. 
To add an additional element, create it, and group it with the VGroup.

.. code :: python

    def build(self):
        inside_text = TextMobject(self.text)
        rectangle   = Rectangle(height=self.height, width=self.width, color=self.color)
        group       = VGroup(inside_text, rectangle)
        return group

Text Box
--------------------

Our Text Box takes in:
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

We have decided to keep track of the line executing with an ArrowTip. If you wish to change that shape, color, or scale, change this line in your construct function.

.. code :: python

    def construct(self):
        ...
        pointer = ArrowTip(color=YELLOW).scale(0.7).flip(TOP)

We are going to the next line by calling the ``move_arrow_to_line`` function. To change the moment at which you change the line number, you can move this line.