pipeline {
    agent any

    environment {
        IMAGE_NAME = "hello-devops"
        IMAGE_TAG = "1.0"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                echo "Running Maven Build..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                echo "Building Docker image..."
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Docker Run & Test') {
            steps {
                echo "Running Docker container..."
                sh 'docker run --rm $IMAGE_NAME:$IMAGE_TAG'
            }
        }

        stage('Push to Registry') {
            when {
                branch 'main'
            }
            steps {
                echo "You can add image push step here if Docker Hub or Nexus configured"
                // Example:
                // sh "docker tag $IMAGE_NAME:$IMAGE_TAG your-repo/$IMAGE_NAME:$IMAGE_TAG"
                // sh "docker push your-repo/$IMAGE_NAME:$IMAGE_TAG"
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
