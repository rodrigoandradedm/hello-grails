#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage('setup') {
            steps {
                git branch: 'master', url: 'http://10.250.14.1:8929/root/hello-grails'    
            }                 
        }
        stage('Test') {
            steps {
                sh './gradlew -Dgeb.env=firefoxHeadless iT'
            }
            post {
                always {
                    publishHTML(
                        target: [
                        allowMissing         : false,
                        alwaysLinkToLastBuild: false,
                        keepAll              : true,
                        reportDir            : 'build/reports/codenarc/',
                        reportFiles          : 'test.html',
                        reportName           : "Codenarc Report"
                        ]
                    )
                }
            }                
        }
    }
}
