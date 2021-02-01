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
                    step(pitmutation 
                        killRatioMustImprove: false, 
                        minimumKillRatio: 50.0, 
                        mutationStatsFile: 'build/reports/pitest/mutations.xml')
                }
            }

        }
    }
}
