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
                   sh './gradlew clean check'
                }
            }
            post {
                always {
                   recordIssues enabledForFailure: true, tool: spotBugs(pattern: 'build/reports/spotbugs/*.xml')
                 }
            }
        }   
    }
}
