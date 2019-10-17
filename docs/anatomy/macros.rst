Macros
=======

A macro is a set of functions that perform a task. For example, adding a page is a good task to make into a macro because it is a task that is performed throughout many tests.

Macros are structured like most functions within any programming language, except with some minor differences:

  * Macros have no return type unless a string is explicitly returned, but this will not break out of the macro like a normal programming language. All statements after a return will still execute and the return function will only set the return value once the macro finishes executing.
  * Macros can be annotated with the ``@summary`` notation, to inform users of the macro’s purpose.
  * All macros have public access. There is no way to protect another macro file or testcase from accessing your macro. Even by using standard conventions of a helper function with the underscore, other testers are able to use any macro if they want or need to.
  * Since we aren’t using Java Selenium, we also cannot use try-catch blocks to handle any exceptions thrown for weird cases or expected exceptions. If an exception is thrown the test will always fail. Careful decisions are necessary to keep tests stable.

Macros are structured similarly to the paths in the portlet folder. Some of them are separated by component name (currently only Echo macros), but the rest of them have no differentiating factor other than the file name, so reading through file names, and searching with keywords and regular expressions are the best ways to find most macros.

Designing Macros
-----------------
A lot of test fix related failures occur when a test engineer forces a new interaction by adding an extra behavior, like a Navigate step to a macro that performs a simple action. Macros should generally do one thing, regardless of how low or high level it is so that users of the macro can guarantee that it does what it is supposed to do.
Some macros have 20 if statements, some loops, and end up being 50 or more lines long. When macros are not broken up, they become complicated, causing a lot of Poshi tests to be unreadable, fragile and inflexible to future changes.

Extended Macros
----------------
Instead of directly using abstract macros such as ``Button.click()`` directly in your component-specific macro/test cases it may make sense to wrap them inside a macro that calls the generic one. In the case that your component-specific macro gets extended and is no longer the same as the original, it will require only one change instead of a couple hundred nested randomly.
