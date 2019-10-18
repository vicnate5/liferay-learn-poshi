Building a Test File
=====================
Now let’s say we want to add a few more tests to the HelloPoshi.testcase file. In each test, we’ll first need to login to portal. But do we need to copy-paste that same login macro to the beginning of each test? No! This is a great place to leverage the setUp block.

Let’s now add the following block of code just under the property line:

1. ``setUp {}`` While the setUp block isn’t mandatory, it’s very useful, so you’ll notice that we use it in almost all of our testcase files. Within this block, we can put the login macro, and it can be used at the beginning of every test.
2. Remove the login macro from our test{} block and add it under the setUp block. This sets up the all the tests in the testcase file to login first.

  At this point, your test should look like the following:
  ::
definition {
  property testray.main.component.name = "Blogs";

  setUp {
    User.firstLoginPG();
  }

  test ViewHelloWorld {

  }
}

3. Let’s add a test that will add a Blog Entry. Let’s call it ``test AddBlogsEntry {}``
4. Next, let's add macros to navigate to Blogs admin and to add a Blogs entry.
  a. Navigate to Blogs Admin
    .. note::
      In Sublime, If you’ve added the portalweb folder to your project and saved it, you can press ``Ctrl + p`` to open up a quick search
    From the quick search, start typing ‘BlogsNavigator’ until you can scroll to and open it. Most macros in here goto places when already on the Blogs Admin page, look for a macro that starts with open, we can use that.

  b. Add Blogs Entry
    1. Type in ``Ctrl + p`` again, this time inputting ‘Blogs.macro’ - you’ll notice that Sublime grabs everything *including* that string
    2. There are macros for doing specific actions (of a certain kind) to Blogs, like BlogsConfiguration, and BlogsEntryComment, but if we’re not sure, we should start at the top level and work our way down:
    3. Open Blogs.macro.
    4. Notice that Blogs.macro calls other blogs-related macros, the top-most blocks all do some kind of adding, let’s use the generic addEntry block
    5. Notice in addEntry that there are a handful of variables - do we need them all? No, we don’t. Let’s just add the essentials in our test:
      * entryContent
      * entryTitle
    6. Verify variable usage tendencies in Sublime
      * Type ``Ctrl + Shift + F`` to open the advanced search dialog
      * Click the ``.*`` button on the left side (to use regex)
      * Find: ``Blogs.addEntry\(.*\n.*\n.*;`` We add new lines in the search to widen the line context returned in the search (so we can see all the variables)
      * With Sublime scoped to our portalweb folder, we’ll see that, of the 124 matches, a majority of them only use the two variables.

.. note::
  At this point, we can save the test and run our new AddBlogsEntry test using the command we used in the Writing a Test Case portion. If the new AddBlogsEntry test was saved in the HelloPoshi testcase file, run the test using the following command:
  ``$ ant -f build-test.xml run-selenium-test -Dtest.class=HelloPoshi#AddBlogsEntry``

Now that our login macro ``(User.firstLoginPG();)``  is up in the setUp block, let’s make our ViewHelloWorld test do what fits its name.

1. To begin, we would need to apply our path-writing skills to find locators such that we can assert parts of a portlet.
2. Find the Title Header of the Hello World portlet, and assert the string “Hello World.”
3. After that we should apply our macro-writing skills, so other test writers can use our macros after us to assert parts of a portlet
  .. note::
    Clarity, simplicity, and reusability should be guiding principles as we write tests
4. Let’s put this header assertion into the Portlet.macro file
  a. Give it a name like viewHeader
  b. Make it take a variable
  c. Pass in the variable from our testcase level
5. With clarity in mind, we can let others know what our test is intended to do without making them walk through the macro minutiae. We can do this at the test-level by adding an ``@description = “string”`` tag. By convention, we place this outside, but just above, the test block
6. Add a tearDown block. If we’re adding similar assets into portal with different tests that are all written within a single testcase file, it can be a good idea to add a tearDown {} block to the testcase. Think of this block like the other bookend to the setUp block, and just like the setup block, the teardown block is optional. It is helpful to use this block when running tests locally, because we will potentially re-run tests numerous times For more information on the teardown block, see the section on Anatomy of a Poshi Test.

Our HelloPoshi.testcase file now has two tests: ``ViewHelloWorld`` and ``AddBlogsEntry``. Try running each test using the command listed on the Note above. If your test is failing, proceed to the next section of this tutorial to learn how to debug your test.
