pipeline {
    agent { label 'linux-agent' } // run on worker node

    tools {
        maven 'Maven-3.8'
        jdk 'JDK17'
    }

    environment {
        DEPLOY_DIR = "/home/ubuntu/deploy"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "🔹 Cloning source code from Git..."
                git branch: 'main', url: 'https://github.com/<your-username>/<your-repo>.git'
            }
        }

        stage('Build Application') {
            steps {
                echo "🔹 Building project using Maven..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo "🔹 Running tests..."
                sh 'mvn test'
            }
        }

        stage('Deploy Application') {
            steps {
                echo "🚀 Deploying application..."
                sh '''
                    mkdir -p $DEPLOY_DIR
                    cp target/*.jar $DEPLOY_DIR/
                    echo "✅ Deployment complete! JAR copied to $DEPLOY_DIR"
                '''
            }
        }
    }

    post {
        success {
            echo "🎉 Build and deployment successful!"
        }
        failure {
            echo "❌ Build or deployment failed!"
        }
    }
}
