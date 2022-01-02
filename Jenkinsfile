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
             
    }
}
