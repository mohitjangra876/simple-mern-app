pipeline {
    agent any

    parameters {
        string(name: 'GIT_BRANCH', defaultValue: 'main', description: 'Git branch to deploy')
        choice(name: 'DEPLOY_TARGET', choices: ['all', 'frontend', 'backend'], description: 'What to deploy')
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning branch: ${params.GIT_BRANCH}"
                git branch: params.GIT_BRANCH,
                    url: 'https://github.com/mohitjangra876/simple-mern-app.git'
            }
        }

        stage('Build & Deploy') {
            steps {
                sh '''
                echo "Deploy target: ${DEPLOY_TARGET}"

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

    post {
        success {
            echo "Deployment completed successfully"
        }
        failure {
            echo "Deployment failed"
        }
    }
}
