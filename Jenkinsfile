
pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                echo 'Task: Compile the source and package it so later stages have a build artefact to deploy.'
                echo 'Tool: Maven'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Task: Run unit tests on the individual pieces, then integration tests to see if those pieces still work once they are wired together.'
                echo 'Tools: JUnit (unit tests) and TestNG (integration tests)'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Task: Run a static analysis pass so the code is checked against common quality rules before anything is deployed.'
                echo 'Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Task: Scan the project for known vulnerabilities in the source and its dependencies.'
                echo 'Tool: OWASP Dependency-Check'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Task: Copy the packaged build onto a staging server that is close to production.'
                echo 'Tool: AWS CodeDeploy (target: AWS EC2)'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Task: Run integration tests against the staging environment, not just the local build.'
                echo 'Tool: Selenium'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Task: Release the same artefact to the production server if staging looked fine.'
                echo 'Tool: AWS CodeDeploy (target: AWS EC2)'
            }
        }
    }
}
