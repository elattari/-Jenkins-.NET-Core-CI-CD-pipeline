pipeline {
    agent any
     triggers {
        githubPush()
      }
    stages {
        stage('Restore packages'){
           steps{
               sh '/usr/local/bin/dotnet restore WebApplication.sln'
            }
         }        
         stage('Clean'){
           steps{
               sh '/usr/local/bin/dotnet clean WebApplication.sln --configuration Release'
            }
         }    
         stage('Build'){
           steps{
               sh '/usr/local/bin/dotnet build WebApplication.sln --configuration Release --no-restore'
            }
         }
         stage('Test: Unit Test'){
            steps {
               sh '/usr/local/bin/dotnet test XUnitTestProject/XUnitTestProject.csproj --configuration Release --no-restore'
            }
         }
         stage('Publish'){
            steps{
               sh '/usr/local/bin/dotnet publish WebApplication/WebApplication.csproj --configuration Release --no-restore'
            }
         }
    }
}
