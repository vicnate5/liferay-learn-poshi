Testing a Web-based Platform
=============================

Selenium WebDriver
-------------------
Liferay's main product (Liferay DXP) is a web-based portal and digital experience platform solution. Because the product's end user is primarily expected to use the product through its web user interface (UI), testing must be done in the web browser. For test automation, Liferay has chosen to build a framework on top of Selenium WebDriver. WebDriver is one of the most popular open source tools for browser automation, and is the tool recommended by the World Wide Web Consortium (W3C). WebDriver has a flexible and extendable API that is compatible across different web browsers. This tool is the foundation for Poshi.

Page Objects
-------------
Liferay has thousands of functional Poshi tests that must be maintained during product development and through many UI changes. In order to reduce test maintenance time/cost, Poshi uses the "Page Object" design pattern. In this pattern, web elements (or "objects") on a page are defined separately from the tests logic itself. Page objects can also be defined in a reusable way. For example, a page button can be defined and maintained in a single file, and then used in almost any test that needs to click on a page button.
