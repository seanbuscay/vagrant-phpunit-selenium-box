Vagrant PHPUnit and Selenium Box
=========================
*Vagrant Box for running PHPUnit_Selenium Test Cases*

A pre-built Vagrant Box to run automated (headless) web browser tests, using the [Selenium WebDriver](http://docs.seleniumhq.org/projects/webdriver/) and tests written as      [PHPUnit_Selenium Test Cases](http://phpunit.de/manual/4.0/en/selenium.html).

This pre-built box is built with: https://github.com/seanbuscay/vagrant-phpunit-selenium

**Requires: Vagrant 1.5+**

## Example Use Case

1. In your development project, keep a directory with phpunit/selenium test cases
2. From the tests directory init the box, ssh into it, and run the tests from the Vagrant shell

## Installation

*You must have Vagrant 1.5+ installed and running on your system.  If you do not, see [Prerequisites - Vagrant ](#prerequisites---vagrant) below.*

1. Either create a new directory to start your Vagrant Box in, or start it within an existing directory of tests.
2. Initialize the PHPUnit_Selenium Box within the directory:

        vagrant init seanbuscay/phpunit-selenium

3. Run Vagrant Up

        vagrant up --provision
    
**Always start your Vagrant Box with the --provision flag.**  This will ensure a new session is started for headless browser testing.

## Usage

#### Login 

After you have started the Vagrant Box, you may ssh into the box with the following command:

    vagrant ssh

You will be logged into the virtual machine and you should see a prompt like: 

    vagrant@selbox:~$

*Note: If the shell prompts you for a password, enter:* `vagrant`

#### Run Tests

##### Tests Go in a Shared Folder

By default, Vagrant will share your local project directory (the directory with the Vagrantfile) to `/vagrant` on the Vagrant Box.  Your test cases should be placed in this shared folder.  For example, if your vagrant box lives on your machine at: `~/workspace/vagrant-phpunit-selenium`, and your tests are in a directory called, `mytests` then move your tests into `~/workspace/vagrant-phpunit-selenium/`.  

The tests will be located in your local machine at:

    ~/workspace/vagrant-phpunit-selenium/mytests
    
And be accessible within your Vagrant Box at:

    /vagrant/mytests

##### Run the Tests in the Vagrant Box

1. [Login](#login) to your running Vagrant Box.  
2. Change into the shared directory: 

         cd /vagrant
         
3. and then into your desired test directory.  From the example above:

         cd mytests
           
4. Now, run your tests using the [Command-Line Test Runner for PHPUnit](http://phpunit.de/manual/current/en/textui.html). 

#### Example Tests

Since many may be new to phpunit_selenium tests there are two example tests on the box already.  The information below walks you through running the example tests.

##### Run example WebTest Case

After you [login](#login), with `vagrant ssh` and see the Vagrant Box prompt `vagrant@selbox:~$`, run the WebTest case:

    phpunit WebTest

The code for this test may be seen here: https://gist.github.com/seanbuscay/9625193#file-webtest-php

The example test case, "WebTest" will run two tests, using two browser sessions; one in Google Chrome and the other in Firefox. 

The first test, titled "testTitle" will open each web browser and goto google.com.  In each browser, the test will assert the page title should be, "Google".   This test should pass in both web browsers.

The second test, titled "testFail" will open each web browser and goto google.com.  In each browser, the test will assert the page title should be, "Gogle".  Note the misspelling.  Because the page title is not actually "Gogle" the test will fail in both browsers. 

Your terminal output should include something like the following at the beginning of the test case's output:

    PHPUnit 4.0.7 by Sebastian Bergmann.

    .E.E

Each character place is a very short summary of the results of the tests.  The periods show two tests passed and the letter "E" shown twice shows two tests failed.  For more information see: [Chapter 3. The Command-Line Test Runner](http://phpunit.de/manual/current/en/textui.html)

The failed tests will also include details about what failed.  You should see a couple of entries of text like the following:

```
Failed command: assertTitle('Gogle')
Failed asserting that 'Google' matches PCRE pattern "/^Gogle$/".

/home/vagrant/WebTest.php:34
/home/vagrant/WebTest.php:34

Caused by
Failed command: assertTitle('Gogle')
Failed asserting that 'Google' matches PCRE pattern "/^Gogle$/".
    
```
 
Upon a test failure, phpunit_selenium will snap a screenshot of what the browser displays at the point of failure.  Access the examples directory from your host os.  You should see two new images with screenshots of the Google home page.

##### Run example WebTest2 Case

    phpunit WebTest2

The code for this test may be seen here: https://gist.github.com/seanbuscay/9625193#file-webtest2-php

The example test case, "WebTest2" will run one test in FireFox using the PHPUnit_Extensions_Selenium2TestCase test case with the Selenium WebDriver API.

The test titled "testTitle" will open FireFox and goto google.com.  The test will assert the page title should be, "Google".   This test should pass.  You should see output similar to the following:

```
vagrant@selbox:~$ phpunit WebTest2
PHPUnit 4.0.7 by Sebastian Bergmann.

.

Time: 5.07 seconds, Memory: 4.50Mb

OK (1 test, 1 assertion)
```



## Roadmap 

@todo

1.  Add Jenkins server
2. 

## Prerequisites - Vagrant  

#### Step 1: Install Required Software

To get [Vagrant](http://www.vagrantup.com/downloads.html) running on your system, follow these steps:

1. Install VirtualBox - https://www.virtualbox.org/wiki/Downloads
2. Install Vagrant - http://docs.vagrantup.com/v2/installation/index.html
3. *(Optional)* To keep your Vagrant Box Utilities in sync with your Virtual Box Version, install the "vbguest plugin" with the following command: ` vagrant plugin install vagrant-vbguest`

#### Step 2: Verify Vagrant is Installed Correctly

Verify that you have at least version 1.5 of Vagrant. Check your Vagrant version on the command line by running:

    vagrant -v

Verify your vbguest plugin is installed with the following command:

    vagrant plugin list

You should see something like the text below in the list: 
`vagrant-vbguest (0.10.0)`

The output may direct you to update your plugin.  Follow the instructions on the screen to do so.

## Current Versions

@todo
