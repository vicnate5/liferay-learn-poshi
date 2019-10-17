Timesavers
============
Below are a few basic tips on how to save time in the debugging process.

Commenting Out Code
--------------------
It is often unnecessary to run a test completely through to reproduce or validate the results you are looking for. Thus, commenting out test steps to slim down the test could help you debug faster. For example, a test runs through steps that include adding a user, adding a site and then failed at creating a blog entry. For the next test run, since the user and site have already been added, we can comment out the code that runs through those steps and we can start the test at navigating to Blogs to create an entry.

See the `Poshiscript guide`_ for comments usage.

Adjusting Poshi Runner properties
----------------------------------
The poshi-runner.properties file dictates how a test runs. The default settings for Poshi Runner is found `here`_. You can add a poshi-runner-ext.properties file to override current settings.

There are a few properties in this file that can be adjusted to help decrease debugging time.

``timeout.explicit.wait=``
Sets the time (in seconds) before a wait function times out. This is set to 60 seconds by default.

``timeout.implicit.wait=``
Sets the time (in seconds) before a non-wait function times out. This is set to 3 seconds by default.

``test.retry.command.wait.time=3``
Sets the time (in seconds) to wait before retrying element retrieval when elements have turned stale.

``get.location.max.retries=3``
Sets the number of attempts WebDriver will make to a location if the WebElement's location cannot be returned.

``get.location.timeout=5``
Sets the duration of the timeout (in seconds) that WebDriver waits before determining the WebElement's location cannot be returned.

.. _`Poshiscript guide`: https://github.com/liferay/liferay-portal/blob/fbf0974749b7db71504fca52a077d5c6c64242a6/modules/test/poshi-runner/poshi-script.markdown#comments
.. _`here`: https://github.com/liferay/liferay-portal/blob/master/modules/test/poshi-runner/poshi-runner/src/main/resources/poshi-runner.properties
