Test Setup & CI
================
Debugging Poshi may be hard without first understanding what happens before test runs. Through some Apache Ant wizardry, we’re able to manipulate files in our test bundles and set up third-party integration among other things. First, let's take a look at properties within Poshi that we can use to modify how the tests run.

Properties within Poshi
------------------------
Property assignments are variables that are intended to be used externally, outside of the actual test context. Properties are typically used to filter tests that get run for different jobs, as well as denote additional logic that must be run outside of the test context before or after a test. Generally, that logic can be found in build-test.xml or other build-test files. Below are some common use cases for properties; other test properties that can be set can be found in the `test.properties`_ file.

``property portal.acceptance = "true";``
  The most common usage of properties is to define which jobs the tests are executed on.


``property app.server.types = "tomcat";``
  Properties can be used to determine how a functional test is executed. Some available options include specifying databases, app servers, and search engines.

``property osgi.module.configurations = "clusterName=&quot;LiferayElasticsearchCluster1&quot;";``
  Additional configurations can be set for portal-ext.properties and osgi config files using properties. This also includes creating osgi config files.


``property osgi.app.includes = "portal-search-solr7";``
  Certain modules and plugins aren’t bundled by default, which require additional logic to deploy them to the test bundle.


``property remote.elasticsearch.enabled = "true";``
  Some tests require additional setup using Ant scripts, generally found in ``build-test-*.xml`` files. An example of this is setting up a remote Elasticsearch server for certain search tests.

``property testray.main.component.name = "Web Search";``
  When the results from a test run are imported to Testray, the property testray.main.component.name defines the component name of the test.

``Property test.name.skip.portal.instance = “Elasticsearch6#OSGiConfigSmokeTest”;``
  By default, we run 3 functional tests per bundle by using portal instances unless ``test.name.skip.portal.instance`` is specified. This negates the need to properly teardown instances.


.. _`test.properties`: https://github.com/liferay/liferay-portal/blob/master/test.properties
