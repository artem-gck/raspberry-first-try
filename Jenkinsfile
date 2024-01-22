#!/usr/bin/env groovy
pipeline {
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
                bat "dotnet restore ${workspace}\\First try.sln"
            }
        }

        stage('Clean') {
            steps {
                bat "msbuild.exe \"${workspace}\\First try.sln\" /nologo /nr:false /p:platform=\"x64\" /p:configuration=\"release\" /t:clean"
            }
        }

        stage('Build') {
            steps {
                bat "msbuild.exe \"${workspace}\\First try.sln\" /nologo /nr:false  /p:platform=\"x64\" /p:configuration=\"release\" /t:clean;restore;rebuild"
            }
        }
    }
}