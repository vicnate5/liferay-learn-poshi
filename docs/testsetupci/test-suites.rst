Test Suites
============

Keeping track of thousands of test cases is cumbersome. Test suites allow you to organize test cases by testing needs instead of monitoring individual tests and the tests that are related to them. For example, if feature A depends on feature B and C, there might be test suites for B and C individually and another test suite to make sure A, B, and C work together

Test suites are comprised of the test cases created in the test planning phase. A well-rounded test suite may span multiple test types and include tests from cross-cutting components. In addition to test cases, test suites may contain test parameters like environment, version, and test properties.

The goal of test suites is to increase the team’s productivity by providing a means for quickly testing and reviewing code.

Specifying Which Tests Run in a Test Suite
-------------------------------------------
First things first, we need to come up with a descriptive test suite name. Our typical convention is to name the suite after the feature that’s being tested. If there are multiple suites created for one feature, we’ll add a hyphen followed by a descriptor (i.e. search-solr). Work with your product team to create a name that is intuitive for them.

`test.batch.names[testsuitename]`_
  * Start by defining which test batches the test suite will be comprised of. Test batches are a list of individual tests grouped by test type, domain, and/or scenario. `Here's a full list of batches`_.
  * In general, the best practice is to include a good mix of backend and frontend tests. General batches like js-unit and semantic-versioning should also be included to catch failures that may affect everyone’s PRs.

`test.batch.class.names.includes[testsuitename]`_
  * Next we’ll want to narrow down which backend tests run in each backend test batch. If we didn’t specify this test property, we would run tests from unrelated components. The easiest way to do this is to come up with a list of tests to include.
    ::
      modules/apps/bookmarks/bookmarks-test/src/testIntegration/java/com/liferay/bookmarks/trash/test/BookmarksFolderTrashHandlerTest.java
      modules/apps/document-library/document-library-test/src/testIntegration/java/com/liferay/document/library/trash/test/DLFileEntryTrashHandlerTest.java
      modules/apps/document-library/document-library-test/src/testIntegration/java/com/liferay/document/library/trash/test/DLFolderTrashHandlerTest.java

  There may be patterns in which case we can use `globs`_ to generalize the expression(s).
  ``**/*TrashHandlerTest.java``

.. warning::
      Be careful of over-generalizing! This might result in the test suite catching too many tests. Thankfully there’s also a way to exclude tests if this happens. See below.

`test.batch.class.names.excludes[testsuitename]`_
  Following the same principles as test.batch.class.names.includes, create a list of tests to exclude from the ones included with the test properties above. Then use globs to consolidate the expression(s).

`test.batch.run.property.query[testbatchname][testsuitename]`_
  Filter functional tests with `Poshi Query Language (PQL)`_.

`test.batch.dist.app.servers[testsuitename]`_
  If the test suite needs to be run on multiple app servers, add them here. Otherwise Tomcat usually suffices.

Stable Suite / Stable Job
--------------------------
As the name suggests, this is a set of stable tests (across all components) that run against every commit. All liferay-portal master(-private) and 7.2.x(-private) pull requests submitted to Brian Chan are merged to ``brianchandotcom/liferay-portal`` and ``brianchandotcom/liferay-portal-ee`` where they undergo a battery of automated tests. When all stable tests pass, the batch of changes are automatically merged to liferay/liferay-portal and/or liferay/liferay-portal-ee.

The first version of the test suite only included compiling portal and running a single functional smoke test. However, the test coverage has since increased with the addition of some upgrade tests and select backend unit/integration tests.

Relevant Suite
--------------
The purpose of this test suite is to run only tests that are relevant to a particular pull request. It was made in an effort to reduce the amount of load caused by the pull request tester running ``ci:test``. This suite should be used as a last resort when no other test suite is applicable to a set of changes. Generally component team test suites are more targeted than relevant and should be used as the preferred test suite.

This suite will run a different set of tests based on the changed code within a particular pull request. It creates a targeted list of tests based off of the modules that were modified based off of this set of rules:

* For the ``module-integration`` & ``module-unit`` tests, it will only run the tests found within changed module groups. (i.e. Journal, Blogs, Portal Workflow, etc.)
* For the "integration" & "unit" tests, if there are any changes outside of the modules folder all of these tests will be ran.
* There is an additional set of test batches that will run no matter what changes have been made within the pull request.

For each changed module group, the specific tests to be included are defined at the module group's test.properties file.

.. _`test.batch.names[testsuitename]`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L2026-L2036
.. _`Here's a full list of batches`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L1151-L1227
.. _`test.batch.class.names.includes[testsuitename]`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L1990-L2022
.. _`globs`: https://docs.python.org/3/library/glob.html
.. _`test.batch.class.names.excludes[testsuitename]`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L1984-L1988
.. _`test.batch.run.property.query[testbatchname][testsuitename]`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L2042-L2046
.. _`Poshi Query Language (PQL)`: https://github.com/liferay/liferay-qa-ee/blob/liferay-qa-docs/tutorials/training/04-auto-analysis/pages/19-pql.markdown
.. _`test.batch.dist.app.servers[testsuitename]`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/test.properties#L2024
