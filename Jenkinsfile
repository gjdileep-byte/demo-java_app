
pipeline {
  agent any
  environment {
    DOCKERHUB_USER = 'dileepgj'
    IMAGE          = 'day1-demo'
  }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Test')     { steps { sh 'mvn -B clean test' } }
    stage('Package')  { steps { sh 'mvn -B package -DskipTests' } }
    stage('Build Image') {
      steps { sh 'docker build -t $DOCKERHUB_USER/$IMAGE:$BUILD_NUMBER .' }
    }
    stage('Push to Docker Hub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds',
            usernameVariable: 'DH_USER', passwordVariable: 'DH_TOKEN')]) {
          sh '''set +x
echo "$DH_TOKEN" | docker login -u "$DH_USER" --password-stdin
docker push "$DOCKERHUB_USER/$IMAGE:$BUILD_NUMBER"
docker logout'''
        }
      }
    }
  }
  post { always { archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true } }
}
EOF
