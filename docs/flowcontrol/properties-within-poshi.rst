Properties within Poshi
========================

What can be set within a testcase file?
---------------------------------------

Annotations in Poshi Script are used to store additional metadata for testcases and testcase files. The syntax is similar to an assignment with the annotation variable being prepended by an ``@``, followed by an ``=``, then followed by a double quoted string of the value.

- ``@component-name:`` Every testcase file requires a component-name annotation. Valid component names can be found here.
- ``@description:`` This is used to describe the use case of the test or macro.
- ``@ignore:`` When set to true, this annotation will disable one or all tests, depending on where it’s declared.
- ``@ignore-command-names:`` This is used to disable tests in a comma delimited list.
- ``@priority:`` This is used to determine the rough fix priority of bugs discovered within functional tests. LRQA test scores are the sum of all corresponding functional tests priorities.

Property assignments are variables that are intended to be used externally, outside of the actual test context. Properties are typically used to filter tests that get run for different jobs, as well as denote additional logic that must be run outside of the test context before or after a test. Generally, that logic can be found in build-test.xml or other build-test files. Below are some common use cases for properties.

- The most common usage of properties is to define which jobs the tests are executed on.
  ``property portal.acceptance = "true";``
- Properties can be used to determine how a functional test is executed. Some available options include specifying databases, app servers, and search engines.
  ``property app.server.types = "tomcat";``
- Additional configurations can be set for portal-ext.properties and osgi config files using properties. This also includes creating osgi config files.
  ``property osgi.module.configurations = "clusterName=&quot;LiferayElasticsearchCluster1&quot;";``
- Certain modules and plugins aren’t bundled by default, which require additional logic to deploy them to the test bundle.
  ``property osgi.app.includes = "portal-search-solr7";``
- Some tests require additional setup using Ant scripts, generally found in ``build-test-*.xml`` files. An example of this is setting up a remote Elasticsearch server for certain search tests.
  ``property remote.elasticsearch.enabled = "true";``
- When the results from a test run are imported to Testray, the property ``testray.main.component.name`` defines the component name of the test.
  ``property testray.main.component.name = "Web Search";``

Do annotations and properties have scopes?
------------------------------------------

Annotations don’t exactly have scopes since most are valid for only one type of code block. The only exception is ``@ignore``, which can have a local or global scope depending on where it was declared; annotations can be declared just above a test block or the definition block. Below is a list of annotations and valid code blocks.

- ``@component-name: definition block``
- ``@description: test block``
- ``@ignore: definition block, test block``
- ``@ignore-command-names: definition block``
- ``@priority: test block``

Like var assignments, properties can have local or global scopes depending on where they’re declared. Properties are declared first within a code block. In general, global properties are most commonly used to determine which jobs to execute tests on and to define Testray component names. Local properties can vary depending on the needs of the test.

- Global property
  ``property testray.main.component.name = "Elasticsearch Impl";``
- Local property
  ``property remote.elasticsearch.enabled = "true";``
