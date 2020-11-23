pipeline {
    agent any
    tools {
        go 'go1.15'
    }
    environment {
        GO115MODULE = 'on'
        CGO_ENABLED = 0 
        GOPATH = "${JENKINS_HOME}/jobs/${JOB_NAME}/builds/${BUILD_ID}"
    }
    stages {        
        stage('Pre Test') {
            steps {
                echo 'Installing dependencies'
                sh 'go version'
                sh 'go get -u golang.org/x/lint/golint'
            }
        }
        
        stage('Build') {
            when {
                anyOf { branch 'master'; branch 'staging' }  
            }
            steps {
                echo 'Compiling and building'
                sh 'go build'
            }
        }

        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploy the app'
                sh './main'
            }
        }
        
    }  
}
