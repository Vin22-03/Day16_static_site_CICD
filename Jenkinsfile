pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        BUCKET_NAME = 'vin-static-site-86673444'       // 🔁 Replace with your actual bucket name
        DISTRIBUTION_ID = 'ET340CYP2M0JL'         // 🔁 Replace with your CloudFront Distribution ID
    }

stages {
        stage('Upload to S3') {
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding',
                    credentialsId: 'aws-creds',
                    usernameVariable: 'AWS_ACCESS_KEY_ID',
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY']]) {

                    sh '''
                    aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                    aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                    aws s3 sync . s3://$BUCKET_NAME/ --exclude "terraform/*" --exclude "Jenkinsfile" --delete
                    '''
                }
            }
        }
        stage('Invalidate CloudFront Cache') {
            steps {
                sh '''
                echo "Invalidating CloudFront cache..."
                aws cloudfront create-invalidation \
                    --distribution-id $DISTRIBUTION_ID \
                    --paths "/*"
                '''
            }
        }
    }
}
