WebDriverImpl (.java)
=====================

BaseWebDriverImpl
------------------
`BaseWebDriverImpl`_ is an abstract base class that implements both LiferaySelenium and WebDriver as stated in the Poshi Layers section. Since this is an abstract base class, Poshi cannot directly execute this WebDriver class, it has to use extended versions of it such as FirefoxWebDriverImpl. This is done to force Poshi to only run tests using browser supported frontend methods.

This is an example of an older but easily explainable example:
::
    @Override
    public void assertElementPresent(String locator) throws Exception{
      if (isElementNotPresent(locator)) {
        throw new Exception(
          "Element is not present at \"" + locator + "\"");
      }
    }

This is an example of the current BaseWebDriverImpl which is cleaner than the previous version:
::
  @Override
  public boolean isElementNotPresent(String locator) {
    return !isElementPresent(locator);
  }

  @Override
  public boolean isElementPresent(String locator) {
    List<WebElement> webElements = getWebElements(locator);

    return !webElements.isEmpty();
  }

#. The assertElementPresent command basically checks if any web element can be found using the locator given by the user, and throws an Exception causing the test to fail if it cannot be found.
#. This is easy to understand if you have Java knowledge, the current implementation uses an innerClass to allow more flexibility on the conditional checks, allowing us to throw specialized exceptions that can be treated as Poshi warnings instead. `See more here`_.

WebDriverImpl
--------------
Each browser will extend BaseWebDriverImpl in a class such as FirefoxWebDriverImpl and override any methods or initializations that may require slight changes due to browser differences. These Browser WebDrivers are the ones that will directly run the Poshi tests and can be found `here`_.

Each implemented public method in ``*WebDriverImpl`` can be executed in the Poshi layer for testers to use, so knowing how they work can be very useful.


.. _`BaseWebDriverImpl`: https://github.com/liferay/com-liferay-poshi-runner/blob/master/poshi-runner/src/main/java/com/liferay/poshi/runner/selenium/BaseWebDriverImpl.java
.. _`See more here`: https://github.com/liferay/com-liferay-poshi-runner/blob/master/poshi-runner/src/main/java/com/liferay/poshi/runner/selenium/BaseWebDriverImpl.java
.. _`here`: https://github.com/liferay/com-liferay-poshi-runner/tree/master/poshi-runner/src/main/java/com/liferay/poshi/runner/selenium
