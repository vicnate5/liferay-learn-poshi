Test Suites
============

What is a test suite?
---------------------

Test suites are comprised of the test cases created in the test planning phase. A well-rounded test suite may span multiple test types and include tests from cross-cutting components. In addition to test cases, test suites may contain test parameters like environment, version, and test properties.

The goal of test suites is to increase the team’s productivity by providing a means for quickly test and reviewing code.

Why test suites?
----------------

Keeping track of thousands of test cases is cumbersome. Test suites allow you to organize test cases by testing needs. For example, if feature A depends on feature B and C, there might be test suites for B and C individually and another test suite to make sure  A, B, and C work together

What is Poshi Query Language (PQL)?
-----------------------------------

Poshi Query Language is a simple query language that will be used to select tests to run for a particular batch. This language was modeled off of JIRA Query Language (JQL).

In order to leverage PQL to create a subset of tests you will need to set a ‘test.batch.property.query[test-batch-here]’ within ‘test.properties’.

See the below example::

  test.batch.property.query[functional-tomcat8-mysql56-jdk8]=\
	 portal.acceptance == true AND \
	  ( testray.component.names == "Blogs" OR testray.component.names == "Blogs Search" )

The above query will group all test commands (i.e. PortalSmoke#Smoke) that have the poshi properties of ‘portal.acceptance’ set to ‘true’, and have the ‘testray.component.names’ of ‘Blogs’ or ‘Blogs Search’ into a list of test commands to be ran for a particular Jenkins job.

.. note::
  The ``\`` character is used to escape the new-line character, meaning that everything is actually a single line. The "\" character is needed at the end of every line (except the very last line) so that the entire query will be treated as a single line.

PQL Components
--------------

When 'poshi properties' are mentioned that is in reference to the properties set within the 'testcase' files.

|image-1|

Field
^^^^^
The 'field' is representative of the poshi properties attributed to each individual 'testcase command'. For a comprehensive list within 'portal' please see look for the ``test.case.available.property.names`` within ``test.properties``.

Operator
^^^^^^^^
The 'operator' is used to relate the 'field' value to the 'value' declared in the query statement.

**Equals (==) | Not Equals (!=)**
    - If a 'test command' has a 'poshi property name' matches the query 'field', and 'poshi property value' matches (does not match) the query 'value' specified that 'test command' will be added to the test set.
    - This 'operator' works with any value.
**Contains (~) | Not Contains (!~)**
    - If a 'test command' has a 'poshi property name' matches the query 'field', and 'poshi property value' contains (does not contain) the query 'value' specified that 'test command' will be added to the test set.
    - This 'operator' only works with string values.
**Greater Than (>) | Greater Than Or Equal To (>=)**
    - If a 'test command' has a 'poshi property name' matches the query 'field', and 'poshi property value' is greater than (or equal to) 'value' specified, then that 'test command' will be added to the test set.
    - This 'operator' only works with numeric values.
**Less Than (<) | Less Than Or Equal To (<=)**
    - If a 'test command' has a 'poshi property name' matches the query 'field', and 'poshi property value' is less than (or equal to) 'value' specified, then that 'test command' will be added to the test set.
    - This 'operator' only works with numeric values.

Value
^^^^^
The 'value' is representative of the value set within your 'test commands'. This will be used to compare within the query.

Keyword
^^^^^^^^
The 'keyword' is used in a similar way that 'conditional operators' are used within java. They allow for more complex queries to include or exclude a certain set of tests.

- **AND**:
  This will act as a logical 'and', meaning if you have 2 conditionals connected by an 'AND' both of those conditions must evaluate as 'true' in order for a test to be included within a set of tests.
- **OR**;
  This will act as a logical 'or', meaning if you have 2 conditionals connected by an 'OR' as long as one of those conditions have been evaluate as 'true' the test will be included within a set of tests.
- **NOT**:
  This will act as a logical 'not', meaning if you have a conditional preceded by a 'NOT' then it will flip the result. Basically, it will turn a 'true' to a 'false'.

How do we specify which tests run in a test suite?
--------------------------------------------------
First things first, we need to come up with a descriptive test suite name. Our typical convention is to name the suite after the feature that’s being tested. If there are multiple suites created for one feature, we’ll add a hyphen followed by a descriptor (i.e. search-solr). Work with your product team to create a name that is intuitive for them.

`test.batch.names[testsuitename]`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  - Start by defining which test batches the test suite will be comprised of. Test batches are the building blocks for any test suite. Here's a full list of batches.
  - In general, the best practice is to include a good mix of backend and frontend tests. General batches like js-unit and semantic-versioning should also be included to catch failures that may affect everyone’s PRs.

`test.batch.class.names.includes[testsuitename]`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  - Next we’ll want to narrow down which backend tests run in each backend test batch. If we didn’t specify this test property, we would run tests from unrelated components. The easiest way to do this is to come up with a list of tests to include.
    ``modules/apps/bookmarks/bookmarks-test/src/testIntegration/java/com/liferay/bookmarks/trash/test/BookmarksFolderTrashHandlerTest.java``
    ``modules/apps/document-library/document-library-test/src/testIntegration/java/com/liferay/document/library/trash/test/DLFileEntryTrashHandlerTest.java``
    ``modules/apps/document-library/document-library-test/src/testIntegration/java/com/liferay/document/library/trash/test/DLFolderTrashHandlerTest.java``
  - There may be patterns in which case we can use globs to generalize the expression(s).
    ``**/*TrashHandlerTest.java``

    .. note::
      Be careful of over-generalizing! This might result in the test suite catching too many tests. Thankfully there’s also a way to exclude tests if this happens.

`test.batch.class.names.excludes[testsuitename]`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  - Following the same principles as test.batch.class.names.includes, create a list of tests to exclude from the ones included with the test properties above. Then use globs to consolidate the expression(s).

`test.batch.run.property.query[testbatchname][testsuitename]`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  - Filter functional tests with Poshi Query Language (PQL)

`test.batch.dist.app.servers[testsuitename]`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  - If the test suite needs to be run on multiple app servers, add them here. Otherwise Tomcat usually suffices.

Stable Suite / Stable Job
-------------------------
As the name suggests, this is a set of stable tests (across all components) that run against every commit. All liferay-portal master(-private) and 7.2.x(-private) pull requests submitted to Brian Chan are merged to ``brianchandotcom/liferay-portal`` and ``brianchandotcom/liferay-portal-ee`` where they undergo a battery of automated tests. When all stable tests pass, the batch of changes are automatically merged to liferay/liferay-portal and/or liferay/liferay-portal-ee

The first version of the test suite only included compiling portal and running a single functional smoke test. However, the test coverage has since increased with the addition of some upgrade tests and select backend unit/integration tests.

Relevant Suite
---------------
The purpose of this test suite is to run only tests that are relevant to a particular pull request. It was made in an effort to reduce the amount of load caused by the pull request tester running  ``ci:test``. This suite should be used as a last resort when no other test suite is applicable to a set of changes. Generally component team test suites are more targeted than relevant and should be used as the preferred test suite.

This suite will run a different set of tests based on the changed code within a particular pull request. It creates a targeted list of tests based off of the modules that were modified based off of this set of rules:

- For the ``module-integration`` & ``module-unit`` tests, it will only run the tests found within changed module groups. (i.e. Journal, Blogs, Portal Workflow, etc.)
- For the ``integration`` & ``unit`` tests, if there are any changes outside of the modules folder all of these tests will be ran.
- There is an additional set of test batches that will run no matter what changes have been made within the pull request.

For each changed module group, the specific tests to be included are defined at the module group's ``test.properties`` file.

.. |image-1| image:: ./img/pql-components.png

.. _test.batch.names[testsuitename]: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L2026-L2036
.. _test.batch.class.names.includes[testsuitename]: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L1990-L2022
.. _test.batch.class.names.excludes[testsuitename]: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L1984-L1988
.. _test.batch.run.property.query[testbatchname][testsuitename]: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L2042-L2046
.. _test.batch.dist.app.servers[testsuitename]: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L2024
