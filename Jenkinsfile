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

                withCredentials([usernamePassword(credentialsId: 'my-temp', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    
                    // some block
                    sh '''
                        aws --version
                        aws s3 ls
                    '''
                }
            }
        }
    }
}
