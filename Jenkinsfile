pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Alanatk/sample-microservice.git'
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                pkill -f "*.jar" || true
                nohup java -jar build/libs/*.jar > app.log 2>&1 &
                '''
            }
        }
    }
}
