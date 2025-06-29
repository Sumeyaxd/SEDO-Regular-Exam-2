pipeline {
    agent any

    environment {
        DOTNET_ROOT = "${HOME}/.dotnet"
        PATH = "${HOME}/.dotnet:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install .NET 8') {
            steps {
                sh '''
                    curl -sSL https://dot.net/v1/dotnet-install.sh -o dotnet-install.sh
                    chmod +x dotnet-install.sh
                    ./dotnet-install.sh --channel 8.0
                '''
            }
        }
        stage('Restore the project') {
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build the project') {
            steps {
                sh 'dotnet build --no-restore'
            }
        }
        stage('Test the project') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
