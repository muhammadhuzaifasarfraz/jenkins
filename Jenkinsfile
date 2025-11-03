pipeline {
    agent any

    environment {
        GIT_CREDENTIALS = credentials('github-token') // Jenkins credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/muhammadhuzaifasarfraz/jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Push Build Folder') {
            steps {
                sh '''
                git config user.name "Jenkins CI"
                git config user.email "jenkins@localhost"
                git add -f  build
                git commit -m "Automated build pushed by Jenkins" || echo "No changes to commit"
                git push https://${GIT_CREDENTIALS_USR}:${GIT_CREDENTIALS_PSW}@github.com/muhammadhuzaifasarfraz/react-jenkins-demo.git HEAD:main
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Build and Push completed successfully!"
        }
    }
}

