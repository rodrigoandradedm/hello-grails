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
                    //sh './gradlew -Dgeb.env=${env.systemProp.geb.env} iT'
                    sh 'echo ${env.systemProp.geb.env}' 
                }
            }
        }
            //post {
              //  always {
                //    publishHTML(
                    //    target: [
                    //    allowMissing         : false,
                    //    alwaysLinkToLastBuild: false,
                    //    keepAll              : true,
                    //    reportDir            : 'build/reports/codenarc',
                    //    reportFiles          : 'test.html',
                    //    reportName           : "Codenarc Report"
                    //    ]
                    //)
                //}
            //}                
        }
    }
}