pipeline {
    agent any
    environment {
        CONTAINER_NAME = 'web3'
        PORT = '91'
    }
    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/Ashu2356/my-web-app.git', branch: 'qa'
            }
        }
        stage('Deploy') {
            steps {
                sh """
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -dit --name ${CONTAINER_NAME} -p ${PORT}:80 httpd
                    docker cp index.html ${CONTAINER_NAME}:/usr/local/apache2/htdocs/index.html
                    docker exec ${CONTAINER_NAME} chmod 644 /usr/local/apache2/htdocs/index.html
                """
            }
        }
    }
}
