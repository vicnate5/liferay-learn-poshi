======================
Learn Poshi
======================

Welcome to Liferay's Poshi training course. What is Poshi? And why do we use it at Liferay? These and other questions will be answered as you go through this course.

Poshi is a tool developed at Liferay that allows test writers to write and automate tests that simulate a real user’s behavior. As we move on through this course, we will learn more about the tools and functionality of Poshi.

.. note:: Need immediate help?

          * Reach someone on the `LRQA Slack channel`_;

          * Ask a Poshi-specific question, on the `Poshi Slack channel`_; or,

          * Refer to the current documentation on our `Github Repo`_.

.. _LRQA Slack channel: https://liferay.slack.com/messages/CL84ZPHAT
.. _Poshi Slack channel: https://liferay.slack.com/messages/CD7939WBE
.. _Github Repo: https://github.com/liferay/liferay-qa-ee/tree/liferay-qa-docs

.. toctree::
  :maxdepth: 1
  :caption: Introduction
  :name: intro

  intro/testing-a-web-based-platform
  intro/poshi-advantage
  intro/poshi-layers
  intro/liferay-functional-testing

.. toctree::
  :maxdepth: 1
  :caption: Anatomy of a Poshi Test
  :name: anatomy-of-a-poshi-test

  anatomy/webdriverimpl
  anatomy/functions
  anatomy/paths
  anatomy/macros
  anatomy/testcases

.. toctree::
  :maxdepth: 1
  :caption: Writing a Test case
  :name: writing-a-test-case

  writing/prerequisites
  writing/writing-a-test-case
  writing/building-a-test-file

.. toctree::
  :maxdepth: 1
  :caption: Debugging
  :name: debugging-poshi

  debugging/workflow
  debugging/reasons-for-failure
  debugging/timesavers
  debugging/verifying-with-ci

.. toctree::
  :maxdepth: 1
  :caption: Test Setup and CI
  :name: test-setup-and-ci

  testsetupci/properties-within-poshi
  testsetupci/test-setups
  testsetupci/test-suites
