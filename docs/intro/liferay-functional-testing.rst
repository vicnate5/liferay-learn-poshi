Liferay Functional Testing
=============================

Test Setup/Execution (ant)
--------------------------
Poshi tests are designed to simulate a real user's behavior, and must be executed against a fully running Portal server. In order to execute these tests, a framework must be in place to start and stop the Poshi executer (known as "Poshi Runner") and the Portal server. The scripts that  handles test and server configuration are found in `Apache Ant`_ scripts in the Portal source root directory.

The easiest way to execute a poshi test on your local machine is to first start a Portal server (Poshi expects the server to be running at localhost:8080 by default), navigate to the Portal source root directory and execute a poshi test using:
``ant -f build-test.xml run-selenium-test -Dtest.class=PortalSmoke#Smoke``

Ant is using the file "build-test.xml", the target "run-selenium-test", and defining the test.class property as the name of the test. The Poshi test name follows the format: ``TestCaseFileName#TestName``. In this case, the file is ``PortalSmoke.testcase`` and the name of the test in that file is "Smoke".

When executing Poshi tests, a released Poshi Runner jar is downloaded, containing the Java layer. This is then executed against the local Test Case files on the executing machine. The non-Java Poshi files are compiled at runtime. Poshi test execution is configurable with ant runtime parameters or using properties found in `test.properties`_.

Current Poshi tests make an assumption when running a test. The test assumes that the portal used for executing the tests does not currently have any data added by a previous user. Know that running poshi on a Portal where other data has already been added (either manually or by another test) may fail due to an unexpected state of the Portal.

Continuous Integration (Jenkins/GitHub)
----------------------------------------
The benefit of automated testing is that tests can be run as many times as needed at any frequency. All of Liferay's Poshi tests are run at least once a day on the development branch. Some of these tests are even run hourly. Liferay has a server farm that can continuously runs Poshi tests (and other types of testing) 24 hours a day. Some tests are run on every single code change. This massive amount of continuous testing is managed by `Jenkins`_ automation servers in the Diamond Bar office.

Additionally, Liferay's GitHub account is connected with a CI bot that allows any Liferay team member to trigger Jenkins execution different suites of tests on code changes sent in a GitHub pull request. Tests will run and report results directly in a comment on the GitHub pull request.

Continuous Results (Testray/Spira)
----------------------------------
As continuous testing is happening, we must be able to collect, parse, and read the test results in a way that helps to make sense of the data received from all the test runs. The current test management solution was developed in-house and is known as `Testray`_. Jenkins test results are sent to Testray where results and history can easily be viewed and analyzed. As of 2019, Liferay QA is in the process of moving test results to a new system that should provide us even more test results clarity and tracking called `SpiraTest`_. Please reach out to your trainer for more information on this.

.. _`Apache Ant`: https://ant.apache.org/
.. _`test.properties`: https://github.com/liferay/liferay-portal/blob/master/test.properties
.. _`Jenkins`: https://jenkins.io/
.. _`Testray`: https://testray.liferay.com/
.. _`SpiraTest`: https://www.inflectra.com/SpiraTest/
