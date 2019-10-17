Functions (*.function)
==========================

In Poshi, a function handles any extra WebDriver commands that an element might require to interact with a page object or element. Consider an example where we would like to toggle a switch and doing so requires the following:
* Wait for SPA refresh on the page;
* Wait for the element to be present on the page;
* Mouse over on the element;
* Check if the toggle has already been enabled/checked, and if not, enable/check the toggle;
* Assert that the enabled/checked toggle is present on the page; and,
* Check for JavaScript or LiferayErrors

Instead of calling all of those methods on a test, a function wraps it all up into a neat little package like in the toggleSwitch function below.

::
    function toggleSwitch{
      WaitForSPARefresh();

      selenium.waitForElementPresent();

      selenium.mouseOver();

      if (selenium.isNotChecked()) {
        selenium.clickAt();
      }

      AssertElementPresent();

      selenium.assertJavaScriptErrors();

      selenium.assertLiferayErrors();
    }

Some things to note about functions:
* All of the functions present in ``*.function`` are either implemented by ``*WebDriverImpl``, or is a function in a ``*.function`` file.
* A method implemented by ``*WebDriverImpl`` can be invoked with the prefix selenium, followed by its method name.
* A function from any ``*function`` file can be invoked with the function filename prefix following the function name. However, like in the example, no function name is required, the default will be used if it is not specified.
* Any Poshi logic such as if statements are executable in this layer.
* Parameters do not need to be passed into the called functions and methods and will be handled correctly by Poshi depending on the function or method invoked.
