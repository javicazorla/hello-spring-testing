pipeline {
    agent any

    stages {
        stage('Build') {

            steps {
                sh './gradlew build'
            }
        }

        stage('Test') {

            steps { 
                sh './gradlew test'
                sh './gradlew pitest'
            }
            post {
                always {
                    steps {
                        pitmutation mutationStatsFile: 'build/reports/pitest/mutations.xml'
                    }    
                }
            }
        }
    }
}
