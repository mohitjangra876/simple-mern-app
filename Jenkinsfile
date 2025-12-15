pipeline {
  agent any

  parameters {
    string(name: 'GIT_BRANCH', defaultValue: 'main', description: 'Git branch to deploy')
    choice(name: 'DEPLOY_TARGET', choices: ['all', 'frontend', 'backend'], description: 'What to deploy')
    choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Environment')
  }

  stages {

    stage("Clone Repository") {
      steps {
        git branch: params.GIT_BRANCH,
            url: 'https://github.com/YOUR_USERNAME/simple-mern-app.git'
      }
    }

    stage("Deploy") {
      steps {
        sh '''
        echo "Deploying branch: ${GIT_BRANCH}"
        echo "Target: ${DEPLOY_TARGET}"
        echo "Environment: ${ENV}"

        if [ "${DEPLOY_TARGET}" = "all" ]; then
          docker-compose down
          docker-compose up -d --build

        elif [ "${DEPLOY_TARGET}" = "frontend" ]; then
          docker-compose build frontend
          docker-compose up -d frontend nginx

        elif [ "${DEPLOY_TARGET}" = "backend" ]; then
          docker-compose build backend
          docker-compose up -d backend nginx
        fi
        '''
      }
    }
  }
}
