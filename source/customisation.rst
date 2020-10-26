Customising Your Animation
=====================================

If you would like to customise the stylistic attributes of your generated animation (for example, the colours of particular variables or data structures), you can create a **stylesheet JSON file** containing your choices.
You can then pass this stylesheet into the compiler using the ``-s`` or ``--stylesheet`` flag. For more on command-line arguments, see the :ref:`Usage section <usage>`.

.. _stylesheet:

Stylesheet
----------

A typical stylesheet may look something like this:

.. code:: json

    {
      "stack1": {
        "textColor": "BLUE",
        "animate": {
            "borderColor": "BLUE"
        }
      },
      "Stack": {
        "borderColor": "YELLOW",
        "animate": {
            "borderColor": "RED",
            "textColor": "RED"
        }
      }
    }

Here, we define two name-value pairs: ``"stack1"`` and ``"Stack"``, which both map to their respective style properties. 

The style properties for ``"stack1"`` are applied to *all* variables in the program *named ``stack1``*, whether in global or local scope. This logic can be extended to all variables throughout the program. 

Meanwhile, the style properties for ``"Stack"`` are applied to *all* variables in the program that are *of the type ``Stack``*, and this again applies throughout all scopes. This works similarly for other data structures. (For a full list of the data structures available in ManimDSL, see :ref:`here <data_structures>`).

Style Properties
^^^^^^^^^^^^^^^^

Here is a definitive list of the style properties you can define in a stylesheet.

Color
~~~~~~~

The following properties take Manim colors* as their values. 

* ``textColor``
* ``borderColor``

These colors can be written in upper case or lower case.

\*For a full list of colors available in Manim, see `here <https://github.com/3b1b/manim/blob/99952067c1a399e15a197310d35a39bb2864b1af/manimlib/constants.py#L199>`_. Please note that any color ending in ``_C`` can be replaced with just the name of the color (for example, ``BLUE_C`` can be written as ``BLUE``).

Animation Properties
~~~~~~~~~~~~~~~~~~~~~



Precedence
^^^^^^^^^^^