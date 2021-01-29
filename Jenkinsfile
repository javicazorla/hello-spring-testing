#!/usr/bin/env groovy

pipeline {
    agent any
    options {
        ansiColor('xterm')
    }

    stages {
        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
    }
}
