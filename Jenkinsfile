#!/usr/bin/env groovy
pipeline {
    agent { node { label 'docker' } }

    environment {
        TEST_PREFIX = "test-IMAGE"
        TEST_IMAGE = "${env.TEST_PREFIX}:${env.BUILD_NUMBER}"
        TEST_CONTAINER = "${env.TEST_PREFIX}-${env.BUILD_NUMBER}"
        REGISTRY_ADDRESS = "my.registry.address.com"

        SLACK_CHANNEL = "#deployment-notifications"
        SLACK_TEAM_DOMAIN = "MY-SLACK-TEAM"
        SLACK_TOKEN = credentials("slack_token")
        DEPLOY_URL = "https://deployment.example.com/"

        COMPOSE_FILE = "docker-compose.yml"
        REGISTRY_AUTH = credentials("docker-registry")
        STACK_PREFIX = "my-project-stack-name"
    }

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
                bat "msbuild.exe ${workspace}\\First try.sln" /t:Build /p:Configuration=Release"
            }
        }

        stage('Build') {
            steps {
                bat "msbuild.exe ${workspace}\\First try.sln /nologo /nr:false  /p:platform=\"x64\" /p:configuration=\"release\" /t:clean;restore;rebuild"
            }
        }
    }

    post { }
}