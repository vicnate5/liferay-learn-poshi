Functions
==========

All of the functions present in ``*.function`` are either implemented by ``*WebDriverImpl``, or is a function in a ``*.function`` file. Example function:
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

A method implemented by ``*WebDriverImpl`` can be invoked with the prefix selenium followed by its method name. A function from any ``*function`` file can be invoked with the function filename prefix following the function name. However, like in the example, no function name is required, the default will be used if it is not specified. Any Poshi logic such as if statements are executable as well in this layer. Parameters do not need to be passed into the called functions and methods, and will be handled correctly by Poshi depending on the function or method invoked.
