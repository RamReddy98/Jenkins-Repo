pipeline {
    agent any

    environment {
        function_name = 'sample-java-app'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Build'
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo 'Test'
            }
        }

        stage('Push') {
            steps {
                echo 'Push'
                sh "aws s3 cp target/sample-1.0.3.jar s3://java-app-backup"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Build'

                sh "aws lambda update-function-code --function-name $function_name --s3-bucket java-app-backup --region us-east-1 --s3-key sample-1.0.3.jar"
            }
        }
    }
}