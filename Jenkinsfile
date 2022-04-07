pipeline {
    parameters {
        string(name: 'branchName', defaultValue: 'main', description: 'Name of the branch which was build.')
        string(name: 'sourceBranchName', defaultValue: 'test_branch', description: 'Name of the source branch which triggers PR build.')
        string(name: 'param1', defaultValue: 'test_param', description: 'Test parameter 1')
        string(name: 'param2', defaultValue: 'test_param', description: 'Test parameter 2')
    }
    agent {
        node {
            label 'master'
        }
    }

    options {
        buildDiscarder logRotator( 
                    daysToKeepStr: '16', 
                    numToKeepStr: '10'
            )
    }

    stages {
        
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }
        
        stage('Prechecks') {
            steps {
                echo "branchName: ${branchName}"
                echo "sourceBranchName: ${sourceBranchName}"
            }
        }

        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: 'https://github.com/msDekova/aws-online-quiz.git']]
                ])
            }
        }

        stage(' Unit Testing') {
            steps {
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}
