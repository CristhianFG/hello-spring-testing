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
                withSonarQubeEnv(credentialsId: '33ec7988-598f-4057-ba67-102150a9cf77', installationName: 'local'){
                         sh './gradlew sonarqube'
                }
            }
        }   
    }
}
