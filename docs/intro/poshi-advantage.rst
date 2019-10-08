Poshi Advantage
================

WebDriver extended
-------------------
Poshi starts with the WebDriver API. Many Poshi methods will be familiar to any tester with Selenium experience. However, Selenium methods are usually primitive to allow a great degree of flexibility. These are intended to be used as a building blocks for helpful web testing tools and functions. Poshi implements and extends WebDriver methods to allow even more helpful functions that even can go beyond the functionality provided by Selenium. This allows new methods that enable Liferay test writers to create tests that easily navigate through the Liferay DXP UI.

Page Objects made easy
----------------------
Embracing the pattern of test logic being seperated from web elements, all page object locators are defined in a single layer in Poshi. This layer maintains all locators and contains a library of hundreds of DXP taglib locators that can be used in any test case. When a Poshi test writer needs to add a new test, it is likely that most of the page objects are already defined.

Simplified syntax
------------------
In order to make it easier for less technical testers to write test automation, Poshi uses a simplified Groovy-like script syntax. It is less verbose than most programming languages and automatically handles importing of other test files. Only the String data type is supported but string manipulation and math operations are still available.
