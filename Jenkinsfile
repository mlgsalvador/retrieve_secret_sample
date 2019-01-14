pipeline {
    agent { label 'ldap' }

    stages {
        stage('Configuration') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'aws_access', variable: 'AWS_ACCESS')]) {
                    sh '''
                    set +x
                    curl -u "$AWS_ACCESS" https://console.aws.amazon.com/secretsmanager/home?region=us-east-1#/secret?name=tutorials%2FMyFirstTutorialSecret
                    '''
                }
            }
        }

        stage('Read_Secret') {
            steps {
                sh 'aws secretsmanager get-secret-value --secret-id tutorials/MyFirstTutorialSecret --version-stage AWSCURRENT > test'
            }
       }
    }
}
