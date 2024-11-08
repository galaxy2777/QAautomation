# Dumitru Simidin - QA Automation Engineer

## 🌟 Professional Overview
Hello! I'm Dumitru, a QA Engineer with over 6 years of experience in manual and automated testing. My expertise lies in web applications, mobile apps, and microservices. I specialize in Robot Framework and am skilled in Python, JavaScript, JMeter, Jenkins, and Docker.

👨‍💻 I love tackling complex problems and simplifying testing workflows.  
🚀 I’m passionate about improving software quality, speeding up delivery times, and helping teams succeed.  
If you're ready to learn how to enhance your test automation, keep reading!

---

## 🛠️ Technologies & Skills
Here's what I work with on a daily basis:

- **Programming Languages**: Python, JavaScript
- **Testing Frameworks**: Robot Framework, Cypress, Selenium WebDriver, JUnit, TestNG
- **CI/CD**: Jenkins
- **Containerization**: Docker
- **Performance Testing**: JMeter
- **Version Control**: Git (GitHub, GitLab)
- **Operating Systems**: Linux (commands for administration and automation)
- **Test Analytics**: Visualizing test metrics using various reporting tools
- **User Acceptance Testing (UAT)**: Creating criteria and getting feedback from stakeholders
- **Project Management**: JIRA (Agile)

---

## 🤖 Test Automation with Robot Framework
Robot Framework is a fantastic open-source tool for test automation. It's simple, readable, and very powerful. You can use it for acceptance testing, robotic process automation (RPA), and much more.

Want to automate your tests with Robot Framework? Here's how you can get started:

### 1. Install Dependencies 🔧
First, you'll need to install Python (if it's not already installed) and the necessary packages.

Run these commands in your terminal:
```bash
pip install robotframework
pip install coverage
robot api_test.robot
```

# Write Your First Test 📝
Now, let’s create your first Robot Framework test. Here’s an example of an API test that checks if you can successfully get and post data from an API.


api_test.robot:
robot
Copiază codul
*** Settings ***
Library    RequestsLibrary
Library    OperatingSystem

*** Variables ***
${BASE_URL}    https://jsonplaceholder.typicode.com

*** Test Cases ***
Test GET Request for Valid User
    [Documentation]  Test the GET API for a valid user.
    ${response}=    GET    ${BASE_URL}/users/1
    Should Be Equal As Numbers    ${response.status_code}    200
    Should Contain    ${response.body}    "Leanne Graham"

Test POST Request for New User
    [Documentation]  Test the POST API to create a new user.
    ${data}=    Create Dictionary    name=John Doe    email=johndoe@example.com
    ${response}=    POST    ${BASE_URL}/users    json=${data}
    Should Be Equal As Numbers    ${response.status_code}    201
    Should Contain    ${response.body}    "John Doe"

Create a Dockerfile for Robot Framework
Here is a simple Dockerfile to containerize your Robot Framework tests:

# Dockerfile:
# Use the official Python image as a base
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements file into the container
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Install Robot Framework
RUN pip install robotframework

# Copy the test files into the container
COPY . .

# Set the default command to run the tests
CMD ["robot", "api_test.robot"]

docker build -t robot-framework-tests .
docker run --rm robot-framework-tests
docker run --rm -v $(pwd)/output:/app/output robot-framework-tests



How to Run Tests in Jenkins in Parallel
Want to speed up your testing by running tests in parallel? Here’s how you can configure Jenkins to do that!

Create a Jenkinsfile in your repository and add the following code to parallelize the test execution:

# groovy



pipeline {
    agent any
    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    // Install necessary dependencies
                    sh 'pip install -r requirements.txt'
                    sh 'pip install coverage'
                }
            }
        }

        stage('Run Tests in Parallel') {
            parallel {
                stage('Run Test Set 1') {
                    steps {
                        script {
                            // Run the first set of tests
                            sh 'coverage run -m robot tests/test_set_1.robot'
                        }
                    }
                }

                stage('Run Test Set 2') {
                    steps {
                        script {
                            // Run the second set of tests
                            sh 'coverage run -m robot tests/test_set_2.robot'
                        }
                    }
                }

                stage('Run Test Set 3') {
                    steps {
                        script {
                            // Run the third set of tests
                            sh 'coverage run -m robot tests/test_set_3.robot'
                        }
                    }
                }
            }
        }

        stage('Publish Coverage Report') {
            steps {
                script {
                    // Generate coverage report
                    sh 'coverage report'
                    sh 'coverage html -d coverage_report'
                    
                    // Publish coverage report in Jenkins
                    publishHTML(target: [
                        reportDir: 'coverage_report',
                        reportFiles: 'index.html',
                        reportName: 'Test Coverage Report'
                    ])
                }
            }
        }

        stage('Publish Test Results') {
            steps {
                script {
                    // Publish Robot Framework results (logs, reports)
                    publishHTML(target: [
                        reportDir: 'output',
                        reportFiles: 'log.html',
                        reportName: 'Robot Framework Report'
                    ])
                }
            }
        }
    }
}



#What's Happening in This Pipeline?
Install Dependencies: We install everything we need, like requirements.txt and coverage.
Run Tests in Parallel: We split the tests into multiple sets and run them in parallel to save time.
Publish Coverage Report: Once tests are complete, we publish the coverage results so you can track how much code is being tested.
Publish Test Results: Lastly, we show the Robot Framework logs and reports in Jenkins.

📊 Generating HTML Reports
After your tests are executed, Robot Framework generates detailed logs and reports. You can view them easily using the publishHTML Jenkins plugin. This provides a summary of test results, including pass/fail statuses and any logs or screenshots.

# Email: simidin95@gmail.com
# LinkedIn: linkedin.com/in/dumitrusimidin-929513147
# Facebook: facebook.com/simidin.dima
# GitHub: github.com/galaxy2777
