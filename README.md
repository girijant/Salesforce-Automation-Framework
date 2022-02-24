# Salesforce-Automation-Framework
A generic BDD framework to automate any Salesforce application(example Nokia ICA-19).

* A BDD based generic framework, developed by using the open-source leading-edge artifacts (Java, Selenium, Cucumber, Spring, REST-Utils ...etc) i.e. used for flawless functional automation (Web-App and Web-Services) of any web application with supported functionalities like UI (Front end of any application), Rest-APIs, SOAP-APIs, SSH, FTP session, Database...etc. This Framework consists of Core Layer and Test Layer (POM Layer + Cucumber Layer).

* The **Core Layer** of this framework is very simple, generic, light-weight and robust with having well rich graphical Reporting format which can be used and enhanced for any product automation.
* The **Test Layer** (POM Layer + Cucumber Layer) of this framework  can be extended or enhanced based on any product's functionalities and automation stratergies.
* This framework can also be easily extended and integrated with any build-tools (Jenkins, Bamboo...etc) for CI/CD and DevOps compliance.

This page is a point of reference to know about the detailed functional Test Automation approach for Nokia Intelligent Care Assistance (ICA) product.

# Prerequisite Skills
Here is the list of prerequisite skills required to understand the this Automation Framework:

* Basic Core Java 
* Eclipse/IntelliJ IDE
* UBDD Utils
* Maven : Configuration, POM.xml, Build-Lifecycle, Phases, Goals…etc
* Log4J : An open-source logging API for java
* Basic Selenium API (WebDriver) 
* Page Object Model(POM) Design Pattern
* Cucumber-Java: Open-source tool for BDD

# Framework Architecture
![image](https://user-images.githubusercontent.com/17194046/155519631-0275f14d-af99-4116-9ff1-a64cb6b0ed06.png)

Salesforce Automation Framework is designed and developed with 5 different layers based on above design diagram. Each layer of this framework is independent, loosely coupled and the detailed description of each layer is below:

**1.UBDD Framework (External Layer - ubdd.jar):**
 An open-source generic Test-Automation core Framework i.e. widely used for flawless web-app/web-service automation across the R&D products: Reducing the manual efforts and Increasing the quality of products in a rapidly changing environment with DevOps compliance.UBDD core framework is a lightweight jar (ubdd.jar) with collection of utils and methods which performs various automation tasks like UI-Automation, Webservice-Automation, Database validation...etc.
- UBDD is integrated with ICA-Automation as a JAR or Maven-dependency with supported version is 'UnifiedBDD-1.0.6-SNAPSHOT.jar'.
- For Salesforce-Automation we instatiate below UBDD-Utils and other utils can be instantiated based on your product's functionalities and automation stratergies:
 a. WebDriverUtils - For UI-Automation using Selenium (WebDriver) api.
 b. RestUtil.java - A REST client with several methods for simulating RESTful Service - Executing REST Requests for static/dynamic data for all media content types, Generating Respons and     validating Body/Header/StatusCode/Error-Message from the Response.

**2.Core Automation Layer:**
The Core layer is encapsulated for configuring the project and instantiating the required UBDD-Utils by using advanced Spring Autowired and Dependency Injection concepts.  Also includes the Page-Base class which is used for:
* Super class of all POM pages. All POM page classes used to inherit the Page-Base class.
* Intilializing WebDriver instance and Page-Factory Instance for all POM pages.
* Commonly used methods being used by POM pages.
![image](https://user-images.githubusercontent.com/17194046/155519991-ac5b7836-bf6c-4ba9-bf6e-8b1c3ac54022.png)

**3.Page-Object-Model Layer(Test Layer):**
* Page Object Model is a design pattern to create Object Repository for web UI elements. Under this model, for each web page in the Salesforce application, there should be corresponding page class (LoginPage, AccountPage, CasePage...etc).
* Each Page class is extending **PageBase** class and will find the **WebElements** of that web page and also contains Page methods which perform operations on those WebElements. **Page Object Model(POM)** helps make the code more readable, maintainable, and reusable.
* **Page Factory** is an optimized inbuilt Page Object Model concept for Selenium WebDriver.
* With the help of PageFactory class, we use annotations **@FindBy** to find WebElement and initElements method is ised to initialize web elements.
![image](https://user-images.githubusercontent.com/17194046/155520430-31123be1-9e9f-41fd-baa9-50e1e17672b6.png)

**4.Cucumber Layer(Test Layer):**
Cucumber is an open-source tool that supports Behavior Driven Development (BDD). It offers a way to write tests/scenarios (Given,When,And,Then...etc) that anybody can understand, regardless of their technical knowledge. Cucumber provides a means to:
* Create Feature files
* Map Step-Definitions to Feature files
* Add Tagging support
* Add Hooks - pre/post scenario, feature, suite (depending on the language you may have more options)
* Run Cucumber feature files
* Data Tables for test-data in Scenario Outlines
* reporting:
  * junit.xml
  * cucumber.json
  * HTML
 ![image](https://user-images.githubusercontent.com/17194046/155520726-7a9c48de-9a05-4616-9db4-69c4cef6d5f9.png)

**5.Execution Layer:**
Helps to execute sinlgle feature-file or the automation-suite based on the specific tags or fetures on multiple browsers. Also executes the entire automation suite through CLI using single maven command. Also generates a well rich graphical Report for success and failure analysis.
![image](https://user-images.githubusercontent.com/17194046/155520847-0e58dd3b-4d2f-4141-81ff-e50411897504.png)

# Framework Detailed Structure:
![image](https://user-images.githubusercontent.com/17194046/155521054-1731bb18-abe7-4c6b-af0b-501fcc37d4c2.png)

# Framework Flow:
Automated Login script execution from the Framework:

1. User has to update the 'project.properties' with the application-url and credentials required to login the application.
2. 'AppConfiguration.java' used to read the 'project.properties' and instantiate the required UBDD-Utils(WebDriverUtils, RESTUtil...etc) needed for UI and webservice automation.
3. Based on the web-applicaion, user has to prepare the POM class files(LoginPage, AccountPage, CasePage...etc) by extending 'PageBase' class for each web page which contains the Object Repository for web UI elements and Page methods to perform multiple operations on those WebElements.
4. User has to create the Cucumber-Feature files(Login.feature) that must be mapped to the required step-definition file(LoginStep.java) which contains the actual test steps/scripts with proper validation.
5. User will run a single cucumber-feature file(Login.feature) or cucumber-suite(based on the tags) from the IDE or CLI:
  * Feature file will trigger the corresponding Step-Definition file.
  * From Step-definition file POM classes will be triggered
  * From each POM class, 'PageBase' class is triggered.
  * From 'PageBase' class, WebDriver instance will be initialized, browser will be initialized, application will be launched and Login script will be executed.
----

# Sample Automated Test Suite Details
![image](https://user-images.githubusercontent.com/17194046/155521806-193015d6-4327-4df7-9c75-cdbcf350424a.png)
![image](https://user-images.githubusercontent.com/17194046/155521865-201b1c26-de54-4944-896c-ae3be58075df.png)
![image](https://user-images.githubusercontent.com/17194046/155521978-96ef4366-6ff1-4c43-9c93-e1928c336da0.png)
![image](https://user-images.githubusercontent.com/17194046/155522030-910a4245-fe0f-42ab-99c8-b46691fe3fee.png)
![image](https://user-images.githubusercontent.com/17194046/155522081-fdaf0228-01d2-4f6d-8b80-ef5856b19718.png)
![image](https://user-images.githubusercontent.com/17194046/155522166-26e75133-c821-4e51-b73d-9b7b40a90fa6.png)

# Ref:
https://confluence.ext.net.nokia.com/display/NSWAppsSystemTeam/ICA+Functional+Test+Automation+Framework

# Demo




