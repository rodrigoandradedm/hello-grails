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
                configFileProvider([configFile(fileId: 'hello-grails-gradle.properties', variable: 'systemProp.geb.env')]) {
                    sh './gradlew test'
                    sh './gradlew integrationTest'

                }
            }
        }
        //post {
        //    always {
        //        publishHTML(
        //            target: [
        //            alwaysLinkToLastBuild: true,
        //            keepAll              : true,
        //            reportDir            : 'build/reports/codenarc/',
        //            reportFiles          : '*.html',
        //            reportName           : "Codenarc Report"
        //            ]
        //        )
        //    }
        //}                
    }
}

