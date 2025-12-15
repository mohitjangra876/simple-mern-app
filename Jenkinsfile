pipeline {
  agent any

  stages {
    stage("Clone Repo") {
      steps {
        git branch: 'main',
            url: 'https://github.com/<YOUR-USERNAME>/simple-mern-app.git'
      }
    }

    stage("Deploy App") {
      steps {
        sh '''
          docker-compose down
          docker-compose up -d --build
        '''
      }
    }
  }
}
