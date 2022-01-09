# 4 Ways To Do Cross-Browser Testing in Java

This repository shows how to do
*[cross-browser testing](https://applitools.com/cross-browser-testing/)*
with [Selenium WebDriver](https://www.selenium.dev/documentation/webdriver/)
in Java in four different ways:

1. Using a local machine
2. Using [Selenium Grid](https://www.selenium.dev/documentation/grid/)
3. Using a cloud testing platform ([LambdaTest](https://www.lambdatest.com/))
4. Using visual testing ([Applitools](https://applitools.com/))

I chose to develop this project using Selenium WebDriver and Java
because they are very popular choices for test automation.
However, these techniques could be done with other tools
(like [Cypress](https://www.cypress.io/) and [Playwright](https://playwright.dev/))
and languages (like C#, JavaScript, Python, and Ruby) as well.


## The main test

This repository contains one main test case that is implemented once
for each of the four ways to do cross-browser testing.

The main test case is a login test for the [Applitools demo app](https://demo.applitools.com).
The steps are:

1. Load the login page.
2. Verify that the login page loads correctly.
3. Perform login.
4. Verify that the main page loads correctly.


## Project setup

This repository is a Java Maven project.
To build the project and run the tests, you will need to install the
[Java Development Kit (JDK) 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html).
It is recommended to use an IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/).


## Running the tests

All tests are located under `src/test/java/com/automationpanda/`.
They are written using the [JUnit 5](https://junit.org/junit5/) framework.
There are 4 test case classes, one for each cross-browser testing method:
Each test has unique setup needs and environment variables (documented below).

You can run tests individually from an IDE like IntelliJ IDEA.
You can also run tests using `mvn test`
(including [single tests](https://maven.apache.org/surefire/maven-surefire-plugin/examples/single-test.html)).
Just remember to set the required environment variables first!


### 1. Using a local machine

Test class: `LocalMachineTest`

Extra setup:

* Install target browsers (Chrome, Firefox, Edge, Safari)
* Install target [browser drivers](https://www.selenium.dev/documentation/webdriver/getting_started/install_drivers/)
  (ChromeDriver, geckodriver, EdgeDriver)

Environment variables:

* `BROWSER`: (optional) `chrome`, `edge`, `firefox`, or `safari`
* `EDGE_DRIVER_PATH`: (required for Edge) the absolute path to EdgeDriver


### 2. Using Selenium Grid

Test class: `SeleniumGridTest`

Extra setup:

* You *must* set up your own Selenium Grid instance
* You could use VMs, containers, or Kubernetes for Selenium Grid infrastructure
* Read the [Selenium Grid docs](https://www.selenium.dev/documentation/grid/) to learn how to set it up
* I used Ubuntu VMs on [Digital Ocean](https://www.digitalocean.com/)
  * 1 VM for the hub
  * 2 VMs for 2 nodes
  * Each node had Chrome and Firefox
  * Config file and launch script copies are located under `segrid/`

Environment variables:

* `BROWSER`: (optional) `chrome` or `firefox`
* `GRID_URL`: the URL for the Selenium Grid instance


### 3. Using a cloud testing platform

Test class: `CloudPlatformTest`

Extra setup:

* You *must* have a LambdaTest account, which you can [register for free](https://accounts.lambdatest.com/register)
* Test results will appear in the LambdaTest dashboard
* Use LambdaTest's [capabilities generator](https://www.lambdatest.com/capabilities-generator/) for env variable values

Environment variables:

* `LT_USERNAME`: your LambdaTest username
* `LT_ACCESS_KEY`: your LambdaTest access key
* `GRID_URL`: (optional) the LambdaTest grid URL
* `BROWSER_NAME`: (optional) the browser name
* `VERSION`: (optional) the browser version
* `PLATFORM`: (optional) the operating system or device
* `RESOLUTION`: (optional) the viewport size


### 4. Using visual testing

Test class: `VisualSnapshotTest`

Extra setup:

* You *must* have an Applitools account, which you can [register for free](https://auth.applitools.com/users/register)
* You can change the cross-browser configurations in the `setUpVisualAI` method
* Test results will appear in the Applitools dashboard
  * The first time you run tests will save baseline snapshots
  * The second time you run tests will compare the latest snapshots against baselines
  * Change `DEMO_SITE` from `original` to `changed` to introduce visual bugs

Environment variables:

* `APPLITOOLS_API_KEY`: your Applitools API key
* `DEMO_SITE`: (optional) `original` or `changed`; the changed site introduces visual bugs