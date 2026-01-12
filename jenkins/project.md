pipeline {
    agent any

    stages {

        stage('Install Packages') {
            steps {
                sh '''
                  sudo apt update -y
                  sudo apt install -y openjdk-17-jdk maven nodejs npm apache2
                  java -version
                  mvn -version
                  node -v
                  npm -v
                '''
            }
        }

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/SauravBagade/DevOps-Projects.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('Student-registration/backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Run Backend') {
            steps {
                dir('Student-registration/backend/target') {
                    // Kill previous running instance if any
                    sh 'pkill -f "java -jar" || true'
                    sh 'nohup java -jar *.jar > app.log 2>&1 &'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('Student-registration/frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                sh '''
                    sudo systemctl start apache2
                    sudo rm -rf /var/www/html/*
                    sudo cp -rf Student-registration/frontend/dist/* /var/www/html/
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Final deployment completed successfully!'
            }
        }
    }
}
