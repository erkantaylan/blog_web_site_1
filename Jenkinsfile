pipeline {
  agent any
  stages {
    stage ('Build') {
      steps {
        sh 'dotnet build'
      }
    }
     stage('Check and Install Entity Framework') {
              steps {
                  sh '''
                      if ! dotnet tool list -g | grep -q "dotnet-ef"; then
                          dotnet tool install --global dotnet-ef
                      else
                          echo "Entity Framework is already installed."
                      fi
                  '''
              }
          }
    stage ('LIST OF TOOLS') {
      steps {
        sh 'dotnet tool list -g'
      }
    }
    stage ('Migration') {
      steps {
        sh 'dotnet ef database update --project "blog_website/blog_website.csproj"'
      }
    }
    stage ('Restore') {
      steps {
        sh 'dotnet restore'
      }
    }
    stage ('Run') {
      steps {
        sh 'dotnet run'
      }
    }
  }
}
