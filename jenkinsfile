pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the repository...'
                checkout scm // 현재 브랜치 소스를 클론
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running the application and saving logs...'

                // simple-app.jar 실행 및 로그 저장
                sh '''
                if [ -f simple-app.jar ]; then
                    echo "simple-app.jar found, starting the application..."
                    java -jar simple-app.jar > app.log 2>&1 &
                    echo "Application is running. Logs are being written to app.log"
                else
                    echo "simple-app.jar not found!"
                    exit 1
                fi
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
