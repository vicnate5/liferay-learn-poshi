Poshi Layers
=============

LiferaySelenium/WebDriverImpl (.java)
--------------------------------------
The first Poshi layer is where WebDriver is implemented in Java. The base class `BaseWebDriverImpl`_ implements both `WebDriver`_ and our own custom interface of selenium methods called `LiferaySelenium`_. Many of the custom methods give the Liferay tester additional functionality, such as waitForConsoleTextPresent, which allows us to check for output in the application server log during test runtime.

Building reliable and reusable functions (.function)
-----------------------------------------------------
While the Java layer has many custom and unique methods, we have reached a point where the base layer is stable and rarely needs any changes. This is partly due to our second layer we call "functions". Functions use a simple syntax to allow testers to combine the primitive methods defined in the Java layer to create reusable functions for test cases that can combine any number of Java methods.

Defining page objects (.path)
------------------------------
Most page object locators are defined in a single layer in Poshi, the "path" layer. This layer only has xpaths and variable names for each xpath. Each path file is named after some taglib, portal page, or broader component. Paths are used in tests by referencing the ``PathFileName#PATH_VARIABLE``. For example, in Button.path, an `xpath`_ is defined for "Close" buttons in the portal. Any test writer can then interact with the "Close" button page object by calling ``Button#CLOSE``.

Scripting user behaviors (.macro)
----------------------------------
Page object interactions are defined in the "function" layer, while page object locators are defined in the "path" layer. The actions and locators are brought together in the "macro" layer. Here is where user interactions are defined. Anything from clicking on a button, to performing navigations, to reading information, or even sending API calls to improve test setup speed. All of this is defined as "macros".

Macro files are generally named after components or parts of components. For example, Liferay has a blog writing and publishing feature. Part of that feature is the individual blog entry. BlogsEntry.macro defines all the user interactions with the entry. The user might need to flag a blog entry for violation of the Terms of Use. A user interaction, "flagPG" (PG means "Page") is defined in `BlogsEntry.macro`_. You will notice that this macro uses the "Close" button page object we referenced in the above section. The "Click" function (defined in `Click.function`_) is executed on the path defined in Button.path resulting in the final code:
::
  Click(locator1 = "Button#CLOSE");

Writing test cases (.testcase)
-------------------------------
Now that all the webdriver/selenium interactions are written, the functions are created, the page object locators are defined, and the user behavior scripted - a test writer is now able to simply write a test case combining user interactions to make sure that the Portal is behaving as expected. A test case is primarily a combination of macros with any variable values defined. Our example macro might be used in a test case like this:
::
  BlogsEntry.flagPG(
    flagReason = "Spam",
    siteName = "Test Site",
    userEmailAddress = "userea@liferay.com");

Test case files also define setup steps, teardown steps, properties, and individual test priorities. Generally a test case file will be organized around a component or component group and may contain multiple test cases. See `example test case`_ for the Calendar component.

.. _`BaseWebDriverImpl`: https://github.com/liferay/liferay-portal/blob/master/modules/test/poshi-runner/poshi-runner/src/main/java/com/liferay/poshi/runner/selenium/BaseWebDriverImpl.java
.. _`WebDriver`: https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/WebDriver.html
.. _`LiferaySelenium`: https://github.com/liferay/liferay-portal/blob/master/modules/test/poshi-runner/poshi-runner/src/main/java/com/liferay/poshi/runner/selenium/LiferaySelenium.java
.. _`xpath`: https://github.com/liferay/liferay-portal/blob/7b453718d11cdefaa9fa25f2fe3d8ec9b3428dbc/portal-web/test/functional/com/liferay/portalweb/paths/pathlib/uielements/Button.path#L146-L150
.. _`BlogsEntry.macro`: https://github.com/liferay/liferay-portal/blob/7b453718d11cdefaa9fa25f2fe3d8ec9b3428dbc/portal-web/test/functional/com/liferay/portalweb/macros/BlogsEntry.macro#L315-L347
.. _`Click.function`: https://github.com/liferay/liferay-portal/blob/7b453718d11cdefaa9fa25f2fe3d8ec9b3428dbc/modules/sdk/gradle-plugins-poshi-runner/samples/src/testFunctional/Click.function
.. _`example test case`: https://github.com/vicnate5/liferay-portal/blob/50041f13102402771a777ae5e31e3364d3ae2b32/portal-web/test/functional/com/liferay/portalweb/tests/enduser/calendar/pgcalendar/CalendarCreateEvent.testcase
