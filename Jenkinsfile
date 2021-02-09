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

        stage('OWASP Dependency-Check') {

            steps { 
                withGradle {
                    sh './gradlew dependencyCheckAnalyze'
                }
            }
            
            post {
                always {
                    dependencyCheckPublisher pattern: 'build/reports/dependency-check-report.xml'
                }
            }
        }

        stage('Test') {

            steps { 
                withGradle {
                    sh './gradlew clean test'
                    sh './gradlew clean check'
                }
            }

            post {
                always {
                    junit 'build/test-results/test/TEST-*.xml'
                    jacoco(execPattern: 'build/jacoco/test.exec')
                    recordIssues(
                        enabledForFailure: true,
                        tool: pmdParser(pattern: '**/build/reports/pmd/*.xml')
                    )

                    recordIssues(
                        enabledForFailure: true,
                        tool: spotBugs(pattern: '**/build/reports/spotbugs/*.xml')
                    )

                }
            }
        }
        
        stage('SonarQube analysis') {
            steps { 
                withSonarQubeEnv(credentialsId: '69314d91-0e1d-4709-9e60-2392f61f2e28', installationName: 'local') {
                    sh './gradlew sonarqube'
                }
            }
        }        
    } 
}
