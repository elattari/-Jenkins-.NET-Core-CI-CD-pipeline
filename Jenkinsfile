pipeline {
    agent any
     triggers {
        githubPush()
      }
    stages {
        
        stage('SonarQube analysis') {
            steps{
               def scannerHome = tool 'sonarqube';
               withSonarQubeEnv('sonarqube') {
                  sh "${scannerHome}/bin/sonar-scanner \
                  -D sonar.login=admin \
                  -D sonar.password=A*P7Jhoz12V2 \
                  -D sonar.projectKey=testNet3 \
                  -D sonar.host.url=http://localhost:9000/"
               }
           }     
        }
        
        stage('Restore packages'){
           steps{
               sh '/bin/dotnet3/dotnet restore WebApplication.sln'
            }
         }        
         stage('Clean'){
           steps{
               sh '/bin/dotnet3/dotnet clean WebApplication.sln --configuration Release'
            }
         }    
         stage('Build'){
           steps{
               sh '/bin/dotnet3/dotnet build WebApplication.sln --configuration Release --no-restore'
            }
         }
         stage('Test: Unit Test'){
            steps {
               sh '/bin/dotnet3/dotnet test XUnitTestProject/XUnitTestProject.csproj --configuration Release --no-restore'
            }
         }
         stage('Publish'){
            steps{
               sh '/bin/dotnet3/dotnet publish WebApplication/WebApplication.csproj --configuration Release --no-restore'
            }
         }
         stage('Deploy'){
             steps{
               sh '''for pid in $(lsof -t -i:9990); do
                       kill -9 $pid
               done'''
               sh 'cd WebApplication/bin/Release/netcoreapp3.1/publish/'
               sh 'nohup /bin/dotnet3/dotnet WebApplication.dll --urls="http://192.168.9.85:9990" --ip="192.168.9.85" --port=9990 --no-restore > /dev/null 2>&1 &'
             }
         }
    }
}
