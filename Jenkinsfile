#!/usr/bin/env groovy
pipeline {
    agent { node { label 'docker' } }

    stages {
        stage ('Clean workspace') {
            steps {
                cleanWs()
            }
        }

        stage ('Git Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/artem-gck/raspberry-first-try'
            }
        }

        stage('Restore packages') {
            steps {
                bat "dotnet restore \"${workspace}\\First try.sln\""
            }
        }

        stage('Clean') {
            steps {
                bat "dotnet clean \"${workspace}\\First try.sln\""
            }
        }

        stage('Build') {
            steps {
                bat "dotnet build \"${workspace}\\First try.sln\" --nologo -c Release /p:Platform=\"Any CPU\""
            }
        }
    }
}