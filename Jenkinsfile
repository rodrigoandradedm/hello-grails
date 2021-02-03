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
            //post {
              //  always {
                //    junit 'build/test-results/integrationTest/*.xml'
                //}
            //}                
        }
        stage('Build') {
            steps {
                sh "./gradlew assemble"
            }
            post {
                success {
                    archiveArtifacts 'build/libs/*.jar'
                }
            }
        }
    }
}
