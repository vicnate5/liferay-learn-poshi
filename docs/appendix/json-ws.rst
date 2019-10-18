JSON-WS with Poshi
===================

Liferay’s Remote Services can be called within Poshi by taking advantage of functions from `JSONCurlUtil.java`_ to send a request to `Liferay’s JSON WS API (JSON Web Service API)`_. Every service within a Model’s ``*ServiceImpl.java`` (`example`_) is available to be invoked unless it contains the annotation ``@JSONWebService(mode = JSONWebServiceMode.IGNORE)``. To view a list of available services, see ``${baseURL}/api/jsonws`` (localhost:8080/api/jsonws).

Advantages
-----------
Making calls to the JSON WS API is a quick and reliable way to modify data within Liferay. Setting up tests through Poshi macros can often be very unstable and slow, so using the JSON WS API will speed up tests and reduce their flakiness by a very large amount.

Disadvantages
--------------
By making a call to the JSON WS API, the test does not go through the UI that is normally used to perform a specific action. There are risks in not testing via the UI so ensure coverage,  a separate test needs to perform the actions via frontend. Developing and debugging on the JSON WS API is also not user-friendly. It may not always be obvious on what each Service does, so investigating what they do may require investigating the Service’s Java code as well as inspecting the database to see how the data gets modified with each call.

Using JSON Macros
------------------
Every file of the format ``JSON${objectName}.macro`` (make sure there is no suffix appended) has a list of callable implemented JSON calls and should have user-friendly parameters allowing it to be easily called within a testcase file directly. Example, in order to add a new public widget page to Liferay, we would call a specific macro from JSONLayout
::
  JSONLayout.addPublicLayout(
    groupName = "Test Site Name",
   	layoutName = "Page Name");

If we then want to add a widget to the widget page, we can call this other macro available in JSONLayout.macro
::
  JSONLayout.addWidgetToPublicLayout(
	 column = "1",
 	 groupName = "Test Site Name",
 	 layoutName = "Page Name",
 	 widgetName = "Blogs");

Using these two simple macros, we created a new page and added a Blogs widget to it within a couple of seconds!

Creating and Updating JSON Macros
----------------------------------

Because JSON Macros can constantly change, the best way to figure out how to update or create a new one is to look through the current ones, and ask questions if there are any doubts or confusion of the implementation. JSON Macros are also very risky to change because of how widespread they are used. It is preferred to keep the macros clean and modular so breaking changes occur less. Some examples are listed below.

`JSONWebcontentAPI.macro`_
  This file contains all of the direct API curls. There are no parameter modifications here because it is possible that the caller may want a specific parameter to not be modified, so we keep the parameters given to us as-is and require the caller to specify the exact macros that they desire.

  For example, this implementation from `JSONGroup.macro`_ implies that groupName must always be the name of a group that is a site. This is limited because groupId is forced to be retrieved by JSONGroup.getGroupIdByName, which can only find groups that are sites. An example of a group that is not a site would be a staging site.

`JSONWebcontentSetter.macro`_
  This file extracts the logic of setting variables for the API call to be made. The macros in here should be smart enough to return the correct parameter needed based on what was passed in.

`JSONWebcontentUtil.macro`_
  This file has more complex utility macros that were extracted into this file in order to help keep the rest of the files clean.

`JSONWebcontent.macro`_
  This file contains all of the calls that users of JSON macros will use. It uses the setter macros to prepare the variables needed to make a clean call from the API macros.

Sample Requests on Liferay
---------------------------
We can go to ``${baseURL}/api/jsonws`` (localhost:8080/api/jsonws) to access the web browser UI for calling JSON Services. In Poshi, we would execute these commands via cURL in the terminal, but we can always test them out quickly using the web browser. There is also info on what curls are available in the browser.

JSON Path
---------
After making a curl via Poshi, a generic JSON response is usually returned. However, we can parse it a bit farther using `JSON Paths`_.

Service Context
----------------
`Service Context`_ is an object in Liferay that is used as a parameter when invoking any service that gives its callers more power. For example, by setting certain parameters within the serviceContext, you can create an asset with tags and categories already mapped to it, or to specify the workflow action we want to execute with it (Save as Draft, Published, Pending, etc).

The Service Context object is formatted the same as a JSON object, however, a lot of the work is already simplified in the method `JSONServiceContextUtil.setServiceContext`_, allowing testers to add any of the already implemented parameters when making their own JSON calls.

.. _`JSONCurlUtil.java`: https://github.com/liferay/com-liferay-poshi-runner/blob/master/poshi-runner/src/main/java/com/liferay/poshi/runner/util/JSONCurlUtil.java
.. _`Liferay’s JSON WS API (JSON Web Service API)`: https://portal.liferay.dev/docs/6-2/tutorials/-/knowledge_base/t/invoking-json-web-services
.. _`example`: https://github.com/liferay/liferay-portal/blob/master/modules/apps/fragment/fragment-service/src/main/java/com/liferay/fragment/service/impl/FragmentEntryServiceImpl.java
.. _`JSONWebcontentAPI.macro`: https://github.com/liferay/liferay-portal/blob/master/portal-web/test/functional/com/liferay/portalweb/macros/json/journal/JSONWebcontentAPI.macro
.. _`JSONGroup.macro`: https://github.com/liferay/liferay-portal/blob/master/portal-web/test/functional/com/liferay/portalweb/macros/json/journal/JSONWebcontentAPI.macro
.. _`JSONWebcontentSetter.macro`: https://github.com/liferay/liferay-portal/blob/master/portal-web/test/functional/com/liferay/portalweb/macros/json/journal/JSONWebcontentSetter.macro
.. _`JSONWebcontentUtil.macro`: https://github.com/liferay/liferay-portal/blob/master/portal-web/test/functional/com/liferay/portalweb/macros/json/journal/JSONWebcontentUtil.macro
.. _`JSONWebcontent.macro`: https://github.com/liferay/liferay-portal/blob/master/portal-web/test/functional/com/liferay/portalweb/macros/json/journal/JSONWebcontent.macro
.. _`JSON Paths`: https://github.com/json-path/JsonPath
.. _`Service Context`: https://portal.liferay.dev/docs/7-1/tutorials/-/knowledge_base/t/understanding-servicecontext
.. _`JSONServiceContextUtil.setServiceContext`: https://github.com/liferay/liferay-portal/blob/master/portal-web/test/functional/com/liferay/portalweb/macros/json/util/JSONServiceContextUtil.macro#L70-L98
