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
            configFileProvider([configFile(fileId: 'hello-spring-testing', targetLocation: 'gradle.properties')]) {
                    withSonarQubeEnv() { // Will pick the global server connection you have configured
                        sh './gradlew sonarqube'
                    }
            }
        }        
    }
   
}
