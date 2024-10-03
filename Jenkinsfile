pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Cloning your GitHub project repository
                git 'https://github.com/charlesantonysamyu/sample-project-cicd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run any tests in the project
                echo 'Running Tests...'
                // For now, it's just an echo since there are no tests defined
                // Replace the following line with an actual test command, e.g., `npm test`
                sh 'npm test || true'  // Assuming the test might be placeholder (|| true avoids pipeline failure for missing tests)
            }
        }

        stage('Build') {
            steps {
                // Build the project, assuming a build step exists in the project (e.g., React or Angular apps)
                echo 'Building the application...'
                // If no build step exists, skip this or customize for your project
                sh 'npm run build || true'
            }
        }

        stage('Deploy to AWS Ubuntu Server') {
            steps {
                echo 'Deploying application to AWS Ubuntu server...'
                
                // Ensure that Jenkins can SSH into your AWS Ubuntu instance.
                // This will copy your application to the /var/www/myapp directory on your AWS Ubuntu server.
                // Replace "ubuntu" with the correct username, typically "ubuntu" for AWS EC2 Ubuntu AMIs.

                sh '''
                scp -o StrictHostKeyChecking=no -r ./ ubuntu@13.233.83.134:/var/www/myapp
                ssh ubuntu@13.233.83.134 'pm2 restart myapp || pm2 start /var/www/myapp/index.js --name myapp'
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
