#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage('setup') {
            steps {
                git branch: 'sonarqube', url: 'http://10.250.14.1:8929/root/hello-grails'    
            }                 
        }
        stage('Test') {
            steps {
		sh './gradlew clean test'
                configFileProvider([configFile(fileId: 'hello-grails-gradle.properties', targetLocation: 'gradle.properties')]) {
                    sh './gradlew integrationTest'
		    sh './gradlew codenarcTest'
                }
		withSonarQubeEnv(credentialsId: '47355589-96b7-4a4d-a3e1-97f149f76f8e', installationName: 'local') {
    			sh './gradlew sonarqube'
		}
            }
            post {
                always {
		    publishHTML (target : [allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'build/reports/codenarc/',
                        reportFiles: 'test.html',
                        reportName: 'Codenarc Test Report',
                        reportTitles: 'Codenarc Test Report'
                    ])
                    //publishHTML(
                    //    target: [
                    //    alwaysLinkToLastBuild: true,
                    //    keepAll              : true,
                    //    reportDir            : 'build/reports/codenarc/',
                    //    reportFiles          : '*.html',
                    //    reportName           : "Codenarc Report"
                    //	]
                    //)
                }
            }
        }                
    }
}

