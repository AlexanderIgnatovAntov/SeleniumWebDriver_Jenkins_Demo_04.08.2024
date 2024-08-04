pipeline {
    agent any

    stages {
        stage('Checkout code') {
            //check the repo
            steps {
                git branch: 'main', url: 'https://github.com/AlexanderIgnatovAntov/SeleniumWebDriver_Jenkins_Demo_04.08.2024'
            }
        }
        stage('Set up .Net Core') {
            //install dot net
            steps {
                bat '''
                echo Downloading .Net 6 Sdk
                curl -l -o dotnet-sdk-6.0.132-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/0c82e7e6-fdde-49f2-a69f-bd986aeafe1b/9ea7411a22e661fff0e61e56a466e484/dotnet-sdk-6.0.132-win-x64.exe
                echo Installing dotnet-sdk-6.0.132-win-x64.exe
                dotnet-sdk-6.0.132-win-x64.exe /quiet /norestart
                '''
            }
        }
        stage('Restore dependencies') {
            steps{
            //install dependencies
            bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }
        stage('Build') {
            steps {
            //build
            bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }
        stage('Run Tests TestProject1') {
            steps {
            //run tests
            bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;logFileName=TestResults.trx"'
            }
        }
        stage('Run Tests TestProject2') {
            steps {
            //run tests
            bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;logFileName=TestResults.trx"'
            }
        }
        stage('Run Tests TestProject3') {
            steps {
            //run tests
            bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;logFileName=TestResults.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])
        }
    }
}