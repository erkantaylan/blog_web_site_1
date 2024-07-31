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
        export PATH="$PATH:/var/lib/jenkins/.dotnet/tools"
        '''
      }
    }
    stage('Dotnet list of Migrations') {
      steps {
        sh 'dotnet ef migrations list'
      }
    }

    stage('Restore Dependencies') {
      steps {
        sh 'dotnet restore blog_website/blog_website.csproj'
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
