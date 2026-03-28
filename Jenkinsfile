pipeline{
    agent any

    stages{
        stage('Deoloy'){

            agent
            {
                docker{

                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint=""'
                }
            }
            steps{

                withCredentials([usernamePassword(credentialsId: 'my-temp', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    
                    // some block
                    sh '''
                        aws --version
                        aws s3 ls
                        echo "Hello S3! how's it goin" > index.html
                        aws s3 cp index.html s3://temp-20260327/index.html
                    '''
                }
            }
        }
    }
}
