@Library('pipeline-library')_
pipeline {
   agent any
   options {
      timeout(unit: 'MINUTES', time: 30)
   }
    environment {
        BUILD_NAME = "test-debian-multibranch"
    }
   stages {
     stage('Pre-check') {
         steps {
            script {
               echo 'This branch: ' + env.BRANCH_NAME
                sh 'wget http://ftp.de.debian.org/debian/pool/main/b/busybox/busybox_1.30.1-6+b3_amd64.deb'
                buildInfoInit(build_name: "test-debian-multibranch", build_number: "${BUILD_NUMBER}")
                artifactoryDebianPush("test-debian-multibranch", "${BUILD_NUMBER}")
            
                
            }
         }
      }
   }
   post {
       always{
         buildInfoPublish(build_name: "test-debian-multibranch", build_number: "${BUILD_NUMBER}")
        }
      cleanup {
         print 'Cleaning up workspace directory...'
         cleanWs deleteDirs: true
      }
   }
}
