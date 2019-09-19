======================
Liferay - Learn Poshi
======================

Welcome to Liferay - Learn Poshi!

Need immediate help?
  * Reach someone on the `LRQA Slack channel`_;
  * Ask a Poshi-specific question, on the `Poshi Slack channel`_; or,
  * Refer to the current documentation on our `Github Repo`_.

.. _LRQA Slack channel: https://liferay.slack.com/messages/CL84ZPHAT
.. _Poshi Slack channel: https://liferay.slack.com/messages/CD7939WBE
.. _Github Repo: https://github.com/liferay/liferay-qa-ee/tree/liferay-qa-docs

Introduction
-------------

.. toctree::
  :caption: Introduction
  :hidden:

  intro/01-testing-a-web-based-platform
  intro/02-poshi-advantage
  intro/03-poshi-layers
  intro/04-liferay-functional-testing

:doc:`intro/01-testing-a-web-based-platform`
  Overview of Selenium WebDriver and Page Object Models.

:doc:`intro/02-poshi-advantage`
  Extending WebDriver, page objects made easy and simplifying syntax.

:doc:`intro/03-poshi-layers`
  Poshi is like an onion. Onions have layers. Poshi has layers too.

:doc:`intro/04-liferay-functional-testing`
  Test execution, Continuous Integration with Jenkins/Github, and Continuous Results with Testray/Spira.

Anatomy of a Poshi Test
------------------------

.. toctree::
  :caption: Anatomy of a Poshi Test
  :hidden:

  anatomy/01-poshi-script-webdriver-methods
  anatomy/02-webdriver-methods-poshi-functions
  anatomy/03-paths
  anatomy/04-macros
  anatomy/05-testcases
  anatomy/06-methods

:doc:`anatomy/01-poshi-script-webdriver-methods`

:doc:`anatomy/02-webdriver-methods-poshi-functions`
  Our base implementation of WebDriver methods.

:doc:`anatomy/03-paths`
  Overview, folder structure, XML Layout, and Path Design.

:doc:`anatomy/04-macros`
  General purpose, Navigation vs Action, Extended Macros, Files Names, and
  Common Mistakes

:doc:`anatomy/05-testcases`
  TODO

:doc:`anatomy/06-methods`
  Usage and how methods are useful.

Writing a Test Case
--------------------

.. toctree::
  :caption: Writing a Test cases
  :hidden:

  writing/01-prerequisites
  writing/02-writing-a-test-case
  writing/03-building-a-test-file

:doc:`writing/01-prerequisites`
  Suggested tools for writing Poshi.

:doc:`writing/02-writing-a-test-case`
  Elements required for Poshi validation.

:doc:`writing/03-building-a-test-file`
  Putting it all together.

Debugging
----------

.. toctree::
  :caption: Debugging
  :hidden:

  debugging/01-workflow
  debugging/02-reasons-for-failure
  debugging/03-timesavers
  debugging/04-verifying-with-ci

:doc:`debugging/01-workflow`
  Overview of the debugging process.

:doc:`debugging/02-reasons-for-failure`
  Investigating causes of failure.

:doc:`debugging/03-timesavers`
  Every minute saved is a minute earned.

:doc:`debugging/04-verifying-with-ci`
  Trust that you're doing a good job; but also, verify with CI.

Flow Control and CI
--------------------

.. toctree::
  :caption: Flow Control and CI
  :hidden:

  flowcontrol/01-properties-within-poshi
  flowcontrol/02-test-setups
  flowcontrol/03-test-suites

:doc:`flowcontrol/01-properties-within-poshi`
  Properties, property hierarchy, ant script setup properties.

:doc:`flowcontrol/02-test-setups`
  High level test setups and test-specific test properties.

:doc:`flowcontrol/03-test-suites`
  Purpose, globs, batches, overriding, and organizing test suites.
