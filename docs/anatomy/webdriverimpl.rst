WebDriverImpl (.java)
=====================

This section further discusses the layers, or parts, that make up a Poshi test. For a general overview, see the Poshi Layers section in the Introduction.

BaseWebDriverImpl
------------------
The `BaseWebDriverImpl`_ is an abstract base class that implements both LiferaySelenium and WebDriver as stated in the Introduction to Poshi section.

In the example below, which is from an older version of BaseWebDriverImpl,  the assertElementPresent command checks if any web element can be found using the locator given by the user and throws an Exception causing the test to fail if it cannot be found. This implementation uses an innerClass to allow more flexibility on the conditional checks allowing Poshi to throw specialized exceptions that can be treated as Poshi warnings.
::
    @Override
    public void assertElementPresent(String locator) throws Exception{
      if (isElementNotPresent(locator)) {
        throw new Exception(
          "Element is not present at \"" + locator + "\"");
      }
    }

The following example performs the same function as the one above but uses the current version of BaseWebDriverImpl.
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

WebDriverImpl
--------------
Because this BaseWebDriver is an abstract base class, Poshi cannot directly execute this WebDriver class. Each browser will extend BaseWebDriverImpl in a class such as FirefoxWebDriverImpl and override any methods or initializations that may require slight changes due to browser differences. These Browser WebDrivers are the ones that will directly run the Poshi tests and can be found `here`_.


.. _`BaseWebDriverImpl`: https://github.com/liferay/com-liferay-poshi-runner/blob/master/poshi-runner/src/main/java/com/liferay/poshi/runner/selenium/BaseWebDriverImpl.java
.. _`here`: https://github.com/liferay/com-liferay-poshi-runner/tree/master/poshi-runner/src/main/java/com/liferay/poshi/runner/selenium
