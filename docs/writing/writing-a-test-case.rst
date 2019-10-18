Writing a Test Case
====================
**First**, create a file in ``portal-web/test/functional/com/liferay/portalweb/tests``, call it HelloPoshi.testcase.

.. note::
    InitCaps, where the first letter of each word is a capital letter, is an unenforced convention - the testcase and tests within the testcase file can technically be named just about anything with ASCII chars but it is best to keep a standard.

**Next**, add the following elements that are required by poshi syntax validation. Start your test by opening the ``definition{}`` block. Within the definition{} block, add the following:

1. ``property testray.main.component.name = "Blogs"`` - This property is required syntax for validation and will be covered in Test Setup and CI.
2. ``test ViewHelloWorld {}`` - This should be added on a next line below the property mentioned in step 1.
3.  ``User.firstLoginPG();``
    This goes within ViewHelloWorld {}. This macro is very widely used, and will unlock the door to portal. Note, that in order to make the test do anything, we must add one of two things: a function, and a macro. For more information on functions and macros, see the section on Anatomy of a Poshi Test.

At this point, your test should look like the following:
::
  definition {
    property testray.main.component.name = “Blogs"

    test ViewHelloWorld {
      User.firstLoginPG();
    }
  }

.. note::
    It is good practice to save Poshi files frequently and to validate Poshi syntax early and often by running the following command from portal source root dir: ``ant -f build-test.xml run-poshi-validation``

Now save the file, and let’s run our test!

Running the Test
-----------------
With Portal running on a separate console/terminal instance, open another instance of console/terminal and run the following command from portal root directory:

``$ ant -f build-test.xml run-selenium-test -Dtest.class=HelloPoshi#ViewHelloWorld``

Sit back and watch the automated test login to portal.
