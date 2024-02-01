pipeline {
    agent any

    environment {
        IMAGE_URL   = 'https://samples-files.com/samples/Images/jpg/480-360-sample.jpg'
        OUTPUT_PATH = 'downloaded-image.jpg'
    }

    stages {
        stage('Download Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'my-aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                                     string(credentialsId: 'my-aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                        
                        sh """
                            curl -o ${OUTPUT_PATH} -u ${AWS_ACCESS_KEY_ID}:${AWS_SECRET_ACCESS_KEY} ${IMAGE_URL}
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Image downloaded successfully!'
        }
        failure {
            echo 'Failed to download image.'
        }
    }
}
