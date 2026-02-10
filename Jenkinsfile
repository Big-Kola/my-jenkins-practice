pipeline {
    agent any

    tools {
        maven 'maven-3.9.12'
    }

    stages {
        stage("build jar") {
            steps {
                echo "building the application..."
                sh 'mvn package'
            }
        }

        stage("build image") {
            steps {
                echo "building the docker image..."
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'USER',
                        passwordVariable: 'PASS'
                    )
                ]) {
                    sh '''
                        echo "$PASS" | docker login -u "$USER" --password-stdin
                        docker build -t bigkola1/kola-demo-app:jma-2.0 .
                        docker push bigkola1/kola-demo-app:jma-2.0
                    '''
                }
            }
        }

        stage("deploy") {
            steps {
                echo "deploying the application..."
            }
        }
    }
}
