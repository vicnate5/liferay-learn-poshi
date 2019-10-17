Testing a Web-based Platform
=============================

Testing a UI
-------------
Liferay's main product (Liferay DXP) is a web-based portal and digital experience platform solution. Because the product's end user is primarily expected to use the product through its web user interface (UI), testing must be done in the web browser. Manual execution of UI testing of a complex product like Liferay DXP quickly becomes unsustainable because of the resources needed to re-test a constantly evolving platform. Automated testing becomes the realistic means to continuously test the product over time and identify regressions.

Selenium WebDriver
-------------------
For UI test automation, Liferay has chosen to build a framework on top of Selenium WebDriver. `WebDriver`_ is one of the most popular open source tools for browser automation, and is the tool recommended by the World Wide Web Consortium (W3C). WebDriver has a flexible and extendable API that is compatible across different web browsers. This tool is the foundation for Poshi.

Page Objects
-------------
Liferay has thousands of functional Poshi tests that must be maintained during product development and through many UI changes. In order to reduce test maintenance time and cost, Poshi uses the "`Page Object`_" design pattern. In this pattern, web elements (or "objects") on a page are defined separately from the test’s logic itself. When UI or behavior changes happen, the test maintainer should not have to update many different test files to account for the change. Instead, a page object is defined in a single location, and all tests referencing that page object can automatically be updated without a large search and replace action.


.. _`WebDriver`: https://www.seleniumhq.org/docs/03_webdriver.jsp
.. _`Page Object`: https://www.softwaretestingmaterial.com/page-object-model/#Page-Object-Model-Design-Pattern
