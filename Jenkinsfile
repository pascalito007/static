
pipeline {
     agent any
     stages {
          stage('AWS Credentials'){
            steps{
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: '828370275182',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
        ]])
                {
                    sh """
                    mkdir -p ~/.aws
                    echo "[default]" >~/.aws/credentials
                    echo "AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}">> ~/.aws/credentials
                    echo "AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}">>~/.aws/credentials
                    """
                }
            }
         }
         stage('Upload to AWS') {
             steps {
                 withAWS(region:'us-west-2',credentials:'828370275182') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'jenkins-pipeline-project')
                  }
             }
         }
     }
}
