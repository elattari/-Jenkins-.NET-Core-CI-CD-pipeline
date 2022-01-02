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
         stage('Deploy'){
             steps{
               sh '''for pid in $(lsof -t -i:9990); do
                       kill -9 $pid
               done'''
               sh 'cd WebApplication/bin/Release/netcoreapp3.1/publish/'
               sh 'nohup dotnet WebApplication.dll --urls="http://192.168.20.110:9990" --ip="192.168.20.110" --port=9990 --no-restore > /dev/null 2>&1 &'
             }
         }
    }
}
