pipeline {
    agent any

    environment {
        APP_SERVER = "APP_SERVER_IP"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Alanatk/sample-microservice.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                scp target/*.jar ubuntu@$APP_SERVER:/home/ubuntu/app.jar

                ssh ubuntu@$APP_SERVER "
                    pkill -f app.jar || true
                    nohup java -jar /home/ubuntu/app.jar > app.log 2>&1 &
                "
                '''
            }
        }
    }
}
