| Code_ | Bugs_ | Forum_ | Docs_ | License_ | Contact_

.. _Code : http://github.com/frgomes/sphinx_typesafe
.. _Bugs : http://github.com/frgomes/sphinx_typesafe/issues
.. _Forum : http://github.com/frgomes/sphinx_typesafe/wiki
.. _Docs : http://sphinx_typesafe.readthedocs.org
.. _License : http://opensource.org/licenses/Apache-2.0
.. _Contact : http://github.com/~frgomes



``sphinx_typesafe`` is a decorator which enables dynamic type checking on Python 
method and function calls. It works in conjunction with `Sphinx-style docstrings`_,
which makes it particularly convenient for keeping the code documentation up-to-date
with the code actually being executed.

.. _`Sphinx-style docstrings`: http://sphinx-doc.org/markup/desc.html#info-field-lists


Features is a Nutshell
======================

* The decorator can be attached to any function or method.

* Raises ``TypeError`` if types of arguments do not match the specification.

* Raises ``TypeError`` if type of return value does not match the specification.

* Performs dynamic type checking.


Python2
=======

Since function annotations are not available in Python2 the way type checking for Python2 is a documentation convention for parameters based on `the info field lists of sphinx`_. So even when you don't use type checking you can use it to generate documentation.

.. _`the info field lists of sphinx`: http://sphinx-doc.org/markup/desc.html#info-field-lists


Syntax for Python2 using sphinx style docstrings
------------------------------------------------

This is the preferred way since you will be also documenting your code.

::

	@typesafe
	def foo(param_a, param_b):
		"""
		:type param_a: 	types.StringType
		:type param_b: 	types.IntType
		:rtype:         types.BooleanType	
		"""
		# Do Something 
		return True


.. note::

    Observe the usage of ``rtype`` to specify the type returned by the function.



Syntax for Python2 using decorator arguments
--------------------------------------------

This is an alternative approach, useful in circunstances where Sphinx-style documentation is not allowed or desired, for whatever reason.

::

	@typesafe( { "param_a" : str, 
		     "param_b" : types.IntType, 
		     "param_c" : own_module.OwnType
		     "return"  : bool }
		     )
	def foo(param_a, param_b, param_c):
		""" Some Docstring Info		 """
		# Do Something 
		return True

.. note::

   Observe the usage of ``return`` to specify the type returned by the function.



You can use any Python type
---------------------------

So if you have defined a ``Point`` class in module ``mod1`` like below:

::

    # File: mod1.py

    class Point(object):
	def __init__(self, x = None, y = None):
            """ Initialize the Point. Can be used to give x,y directly."""
	    self.x = x
	    self.y = y

then you can employ this type in your code like this:

::

   from mod1 import Point

   @typesafe
   def foo(afunc):
       """ 
       :type afunc: 	mod1.Point
       :rtype: 		types.BooleanType
       """
       return True


Python3
=======

.. warning::

    This is a tentative implementation which is not finished at the moment!!


The base technique is the Function Annotations proposed in `PEP-3107`_ which is 
documented in `Python3 What's New`_ (see section New Syntax).


.. _`PEP-3107`: http://www.python.org/dev/peps/pep-3107
.. _`Python3 What's New`: http://docs.python.org/3.0/whatsnew/3.0.html


Syntax for Python3
------------------

::

	@typesafe
	def foo(param_a: str, param_b: int) -> bool:
		# Do Something 
		return True


* The @typesafe decorator will then check all arguments dynamically whenever the foo is called for valid types.

* As a quoting remark from the PEP 3107: "All annotated parameter types can be any python expression.", but for typechecking only types make sense, though.

The idea and parts of the implementation were inspired by the book: `Pro Python (Expert's Voice in Open Source)`_

.. _`Pro Python (Expert's Voice in Open Source)`: http://www.amazon.com/Python-Experts-Voice-Open-Source/dp/1430227575



FAQ
===

Why it was called IcanHasTypeCheck ?
------------------------------------

*IcanHasTypeCheck (ICHTC)*, refers to the `famous lolcats`_.

.. _`famous lolcats`: http://en.wikipedia.org/wiki/I_Can_Has_Cheezburger%3F


Why is now called sphinx_typesafe ?
-----------------------------------

Because *typesafe* tells immediatelly what it is about. Unfortunately, *typesafe* was already taken on PyPI, so *sphinx_typesafe* seemed to be a good alternative name which also relates to the documentation standard adopted.


Support
=======

Please find links on the top of this page.