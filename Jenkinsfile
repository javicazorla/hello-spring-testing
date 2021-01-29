#!/usr/bin/env groovy

pipeline {
    agent any

    options {
        ansiColor('xterm')
    }

    stages {

        stage('Test') {
            steps { 
                withGradle {
                    sh './gradlew test'
                }
            }
        }

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
    }
}
