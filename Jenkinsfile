pipeline {
  agent any
  stages {
    stage ('Build') {
      steps {
        sh 'dotnet build'
      }
    }
     stage ('LIST OF TOOLS 1') {
      steps {
        sh 'dotnet tool list -g'
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
