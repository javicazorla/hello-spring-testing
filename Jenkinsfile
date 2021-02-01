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
                    sh './gradlew clean test'
                }
            }

            post {
                always {
                    pitmutation mutationStatsFile: 'build/reports/pitest/**/mutations.xml'
                }
            }
        }
    }
}
