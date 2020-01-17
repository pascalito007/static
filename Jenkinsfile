
pipeline {
     agent any
     stages {
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
