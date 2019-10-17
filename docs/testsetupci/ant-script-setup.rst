Ant Script Setup
=================

All functional tests run through a ``run-selenium-*`` target and ``run-simple-server`` which are called from the `build-test.xml`_ file. These two targets are extremely versatile and are responsible for the majority of test setup outside of the actual Poshi test. Here are things that are currently possible with these targets.

`run-selenium-tomcat`_
  * Build Tomcat application server
  * Application server configurations for integration tests

`run-simple-server`_
  * Prepare default osgi configurations, portal properties, and system properties
  * Change portal context (URL path portal is located at)
  * Portal SSL setup for testing https
  * Disable dummy proxy which interferes with tests that access external resources
  * Set Tomcat session timeout
  * Start third-party integrations: Elasticsearch, Solr, LDAP, OpenAM, Sharepoint, Documentum, etc
  * Deploy osgi apps (LPKG) or modules (jar)
  * Start multiple bundles
  * Configure clustering if enabled
  * Start application server
  * Run tests
  * Shutdown and stop third-party integrations

.. _`build-test.xml`: https://github.com/liferay/liferay-portal/blob/master/build-test.xml
.. _`run-selenium-tomcat`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/build-test-tomcat.xml#L6-L57
.. _`run-simple-server`: https://github.com/liferay/liferay-portal/blob/6c2e52056617d62b2589e4f23a2cf459feb7b84e/build-test.xml#L10715-L11384
