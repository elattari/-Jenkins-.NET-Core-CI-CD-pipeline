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
    }
}
