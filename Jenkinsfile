pipeline {
  agent any

  environment {
    DOCKERHUB_USER = "pranavdazzler"
    BACKEND_IMAGE = "mern-backend"
    FRONTEND_IMAGE = "mern-frontend"
    SONAR_TOKEN = credentials('sonar-token')
  }

  stages {

    stage('Checkout') {
      steps {
    git branch: 'main',
    url: 'https://github.com/pranavxdevops/mern-budget-tracker-project.git',
    credentialsId: 'github-creds'
      }
    }

    stage('ESLint & Unit Tests') {
      steps {
        sh '''
        cd backend
        npm install
        '''
      }
    }

    stage('npm audit') {
      steps {
        sh '''
        cd backend
        npm audit fix
        '''
      }
    }

stage('SonarQube Analysis') {
  steps {
    sh '''
    docker run --rm \
      -v "$PWD/backend:/usr/src" \
      sonarsource/sonar-scanner-cli \
      -Dsonar.projectKey=Mern \
      -Dsonar.sources=. \
      -Dsonar.host.url=http://65.2.130.138:9000 \
      -Dsonar.login=$SONAR_TOKEN
    '''
      }
    }

    stage('Build Docker Images') {
      steps {
        script {
          docker.build("${DOCKERHUB_USER}/${BACKEND_IMAGE}:${BUILD_NUMBER}", "backend")
          docker.build("${DOCKERHUB_USER}/${FRONTEND_IMAGE}:${BUILD_NUMBER}", "frontend")
        }
      }
    }

    stage('Trivy Scan') {
      steps {
        sh '''
        trivy image ${DOCKERHUB_USER}/${BACKEND_IMAGE}:${BUILD_NUMBER}
        trivy image ${DOCKERHUB_USER}/${FRONTEND_IMAGE}:${BUILD_NUMBER}
        '''
      }
    }

    stage('Push Images') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: 'dockerhub-creds',
          usernameVariable: 'USER',
          passwordVariable: 'PASS'
        )]) {
          sh '''
          echo $PASS | docker login -u $USER --password-stdin
          docker push ${DOCKERHUB_USER}/${BACKEND_IMAGE}:${BUILD_NUMBER}
          docker push ${DOCKERHUB_USER}/${FRONTEND_IMAGE}:${BUILD_NUMBER}
          '''
        }
      }
    }

    stage('Update GitOps Repo') {
  steps {
    dir('gitops') {
      checkout([
        $class: 'GitSCM',
        branches: [[name: '*/main']],
        extensions: [
          [$class: 'LocalBranch', localBranch: 'main']
        ],
        userRemoteConfigs: [[
          url: 'https://github.com/pranavxdevops/mern-budget-tracker-k8s.git',
          credentialsId: 'github-creds'
        ]]
      ])

      sh '''
      cd "Kubernetes files"

      sed -i "s|image: .*mern-backend.*|image: ${DOCKERHUB_USER}/${BACKEND_IMAGE}:${BUILD_NUMBER}|" backend-deployment.yaml
      sed -i "s|image: .*mern-frontend.*|image: ${DOCKERHUB_USER}/${FRONTEND_IMAGE}:${BUILD_NUMBER}|" frontend-deployment.yaml

      git config user.email "jenkins@ci.local"
      git config user.name "Jenkins CI"

      git status
      git add .
      git commit -m "Update image tag to ${BUILD_NUMBER}" || echo "No changes to commit"

      git push origin main
      '''
      }
    }
  }
  }
}
  
