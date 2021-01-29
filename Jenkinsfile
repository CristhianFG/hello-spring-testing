#!/usr/bin/env groovy
pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                withGradle {
                   sh './gradlew build'
                }
                
            }
            post {
                success {
                    archiveartifacts 'build/libs/*.jar'
                }
            }
        }  

        stage('test') {
            steps {
                withGradle {
                   sh './gradlew test'
                }
                post {
                    always {
                        junit 'build/test-results/test/TEST-*.xml'
                    }
                }
            }
        }
        
         
    }
}
