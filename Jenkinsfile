pipeline {
    agent any

    environment {
        CONTAINER_NAME = 'web2'
        PORT = '91'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/Ashu2356/my-web-app.git', branch: 'dev'
            }
        }

        stage('Deploy') {
            steps {
                sh """
                    docker rm -f ${CONTAINER_NAME} || true

                    docker run -dit \
                        --name ${CONTAINER_NAME} \
                        -p ${PORT}:80 \
                        -v \$(pwd)/html:/usr/local/apache2/htdocs \
                        httpd
                """
            }
        }

        stage('Verify') {
            steps {
                sh """
                    docker ps
                    echo "Visit: http://<jenkins-ip>:${PORT}"
                """
            }
        }
    }
}
