#!/usr/bin/env groovy

pipeline {
    agent any

    options {
        ansiColor('xterm')
    }

    stages {

        stage('Build') {
            steps { 
                withGradle {
                    sh './gradlew assemble'
                }

                post {
                    success {
                        archiveArtifacts 'build/libs/*.jar'
                    }
                }
            }
        }

        stage('Test') {
            steps { 
                withGradle {
                    sh './gradlew clean test'
                }

                post {
                    always {
                        junit 'build/test-results/test/TEST-*.xml'
                    }
                }
            }
        }
    }
}
