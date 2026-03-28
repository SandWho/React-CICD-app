pipeline{
    agent any

    stages{
        stage('Deoloy'){

            agent
            {
                docker{

                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrtypoint=""'
                }
            }
            steps{
                sh '''
                    aws --version
                    aws s3 ls
                '''
            }
        }
    }
}
