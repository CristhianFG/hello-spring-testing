pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                withGradle {
                   sh './gradlew assemble'
                }
            }
            post {
                success {
                    archiveArtifacts 'build/libs/*.jar'
                }
            }
        }  

        stage('Test') {
            steps {
                withGradle {
                   sh './gradlew clean test check'
                }
            }
            post {
                always {
                    junit 'build/test-results/test/TEST-*.xml'
                 }
            }
        }

        stage('QA') {
            steps {
                 withGradle{
                     sh './gradlew check'
                 }
            }
            post {
                 always {
                      recordIssues enabledForFailure: true, tool: pmdParser(pattern: 'build/reports/pmd/*.xml')
                 }
            }
        }

        stage('Artefacto'){
            steps {
                 // withCredentials([string(credentialsId: 'gitLabPrivateToken', variable: 'TOKEN')]) {
                    withCredentials([string(credentialsId: 'apacheArchiva', variable: 'username', variable: 'password')]) 
                       sh './gradlew publish'
                 } 
            }
        }     
    }
}
