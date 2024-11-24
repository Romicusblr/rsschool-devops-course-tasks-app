pipeline {
    agent {
        kubernetes {
            yaml """
            apiVersion: v1
            kind: Pod
            metadata:
              name: kaniko
            spec:
              containers:
              - name: kaniko
                image: gcr.io/kaniko-project/executor:debug
                args: ["--dockerfile=Dockerfile", "--context=git://github.com/Romicusblr/rsschool-devops-course-tasks-app.git#refs/heads/task-6", "--context-sub-path=app", "--destination=441592700969.dkr.ecr.us-east-1.amazonaws.com/my-jenkins-app:test", "--oci-layout-path=/kaniko/oci"]
                volumeMounts:
                - name: kaniko-secret
                  mountPath: /kaniko/.docker/
              volumes:
              - name: kaniko-secret
                secret:
                  secretName: ecr-registry
            """
        }
    }

    stages {
        stage('Logging into AWS ECR') {
            steps {
                script {
                    sh """aws ecr get-login-password --region ${AWS_DEFAULT_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com"""
                }
                 
            }
        }
        stage('Build and Push Docker Image') {
            steps {
                echo 'Waiting for 1 minute...'
                sleep time: 1, unit: 'MINUTES'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
