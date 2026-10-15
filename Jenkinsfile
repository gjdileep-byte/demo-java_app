```groovy
pipeline {
    agent any

    tools {
        jdk 'java17'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out from Git'
            }
        }

        stage('Check Java and Maven') {
            steps {
                sh '''
                    echo "Checking Java version"
                    java -version

                    echo "Checking Java compiler"
                    javac -version

                    echo "Checking Maven version"
                    mvn -version
                '''
            }
        }

        stage('Maven Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Package Application') {
            steps {
                sh 'mvn package -DskipTests'
                sh 'ls -lh target/'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
```
