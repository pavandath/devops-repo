## Code Coverage
* As a developer, the teams will be writing source code and we need to test the source code programatically.
* To test the sorce code programatically, the developers will be writing unit test cases.
* Code coverage is nothing but how many lines are tested by the unit test cases written by the developers. 

    * Example: I have a calculator.java with 100 lines of code
    * Devs wrote the unit test cases called `calculatortest.java` and the file has 92 lines of code 
    * Then the code coverage is 92%
    * `Note:` This is one aspect only, there will be multiple aspects and combined into standards and these standards are used for code quality test and this is done by us.

## Code Review
* Sonarqube will be doing code review as well such as:
    * We will be validating code against the standards, to make sure that the devs had written the source code according to standards.
    * Ideally your technical dev leads will takes this up
    * As a devops engineers we need to make sure that our **CICD** has this code quality in place, and make sure we implement those standards as mandatory.
    * To do code review, we are going to use **static code analysis** 

## Sonarqube
* Sonarqube is a third party tool developed by sonar source
* This is a code analysis tool which is aimed to code quality by identifying the issues upfront rather than waiting the application to move to production.