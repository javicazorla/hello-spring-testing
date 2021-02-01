pipeline {
    agent any

    stages {
        stage('Build') {

            steps {
                sh './gradlew assemble'
            }
        }

        stage('Test') {

            steps { 
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
