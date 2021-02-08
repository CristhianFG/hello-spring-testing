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
                configFileProvider([configFile(fileId: 'gradle.properties', targetLocation: 'gradle.properties')]) {
                         sh './gradlew sonarqube'
                  }
            }
        }   
    }
}
