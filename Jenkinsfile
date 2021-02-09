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

        stage('Security') {
            steps {
                sh './gradlew dependencyCheckAnalyze'
            }
        }   
    }
}
