pipeline{
    agent any
    environment{
        NETLIFY_SITE_ID = ''//haii
    }
    stages{
        stage('Build'){
            agent {
                docker{
                    image 'node:24.14.0-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                ls -la
                node --version
                npm --version
                npm install
                npm run build
                ls -la
                '''
            }
        }
        stage('Test'){
            agent {
                docker{
                    image 'node:24.14.0-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
        stage('Deploy'){
            agent {
                docker{
                    image 'node:24.14.0-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm install netlify-cli
                   node_modules/.bin/netlify --version 
                '''
            }
        }

        stage('AWS'){
            agent{
                docker{
                    image 'amazon/aws-cli'
                    reuseNode true
                    args '--entrypoint ""'
                }
            }
            steps{
                WithCredentials([usernamePassword(credentialsId: 'reactAWS', passwordVariable: 'AWS_SECRET')])
                {
                    //some block
                    sh '''
                    aws --version
                    aws 3 ls
                    echo "Hello, s3!" > index.html
                    aws s3 cp index.html s3://bucket-name/index.html
                    '''
                }
            }
        }
    }
}
