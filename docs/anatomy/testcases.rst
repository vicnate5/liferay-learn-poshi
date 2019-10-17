Testcases
=========
Test case = Testclass

Beginning Block
----------------

In every ``*.testcase``, a definition block needs to wrap the entire file with brackets. A component name annotation is needed before every definition block for testray to know which team the testcase file belongs to. Any global properties that will apply to all tests in this testcase file should also be listed here.
::
  @component-name = "portal-wcm"
  definition {

    property portal.release = "true";
    property portal.upstream = "true";
    property testray.main.component.name = "Content Pages";

Setup Block
------------
There is a setup block in each testcase file that runs before each test. This block will perform any setup required to prepare the portal instance for the test, for example, log the admin user in, and then add a new Site to Liferay via JSON
::
  setup {
    TestCase.setUpPortalInstance();

    User.firstLoginPG();

    JSONGroup.addGroup(groupName = "Test Site Name");
  }

Test Block
-----------
Each test can be annotated with a description to describe the test as well as connect it to a jira ticket. Its priority can also be assigned via annotation. Any properties set here will apply to solely the test being run and can override the global testcase properties. For more information on properties, see the Test Setup and CI section of this tutorial.
::
  @description = "This is a test for LPS-101333. Freemarker code should not be executed in an html fragment."
  @priority = "5"
  test AddContentPageWithHTMLFragment
    property portal.acceptance = "true";

    JSONLayout.addPublicLayout(
      groupName = "Test Site Name",
      layoutname = "Content Page Name",
      type = "content");

    ContentPageNavigator.openEditContentPage(
      pageName = "Content Page Name",
      sitename = "Test Site Name");

    PageEditor.editFragmentHTML(
      editableId = "element-html",
      fileName = "fragment_freemarker_basic.html",
      fragmentName = "HTML");

    PageEditor.clickPublish();

    ContentPagesNavigator.openViewContentPage(
      pageName = "Content Page Name",
      siteName = "Test Site Name");

    task ("Assert the freemarker code was not executed") {
      AssertTextNotEquals(
        locator1 = "//div[contains(@class,'fragment-html-test')]",
        value1 = "Basic Test");
    }
  }

Teardown Block
---------------
The tearDown block is executed after every test is completed, whether it passes or not. Using ``PortalInstances.tearDownCP()`` is highly recommended to be executed in case the currently running portal instance is running on CI. This because an instance on CI depends on using virtual hosts to clean up stability and speed improvements.
::
  tearDown {
    var testPortalInstance = PropsUtil.get("test.portal.instance");

    if ("${testPortalInstance}" == "true") {
      PortalInstances.tearDownCP();
    }
    else {
      JSONGroup.deleteGroupByName(groupName = "Test Site Name");
    }
  }
