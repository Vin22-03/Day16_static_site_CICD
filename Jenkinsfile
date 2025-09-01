pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        BUCKET_NAME = 'vin-static-site-86673444'
        DISTRIBUTION_ID = 'ET340CYP2M0JL'
    }

    stages {

        stage('📥 Checkout Code') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/Vin22-03/Day16_static_site_CICD', branch: 'main'
            }
        }

        stage('🔐 Configure AWS Credentials') {
            steps {
                withCredentials([[
                    $class: 'UsernamePasswordMultiBinding',
                    credentialsId: 'aws-creds',
                    usernameVariable: 'AWS_ACCESS_KEY_ID',
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                    sh '''
                    aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                    aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                    aws configure set region $AWS_REGION
                    '''
                }
            }
        }

        stage('🧹 Clean Up Unwanted Files') {
            steps {
                sh 'rm -rf terraform/ || true'
                sh 'rm -rf Jenkinsfile || true'
            }
        }

        stage('📤 Upload Static Site to S3') {
            steps {
                sh '''
                echo "Uploading site to S3..."
                aws s3 sync . s3://$BUCKET_NAME/ \
                  --exclude "terraform/*" \
                  --exclude "Jenkinsfile" \
                  --delete
                '''
            }
        }

        stage('🌀 Invalidate CloudFront Cache') {
            steps {
                sh '''
                echo "Invalidating CloudFront cache..."
                aws cloudfront create-invalidation \
                    --distribution-id $DISTRIBUTION_ID \
                    --paths "/*"
                '''
            }
        }

        stage('✅ Deployment Successful') {
            steps {
                echo '🎉 Site successfully uploaded and cache invalidated!'
            }
        }
    }
}
