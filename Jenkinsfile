#!/usr/bin/env groovy

pipeline {
    agent any

    options {
        ansiColor('xterm')
    }

    stages {

        stage('Test') {
            withGradle {
                sh './gradlew test'
            }
        }

        stage('Build') {
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
