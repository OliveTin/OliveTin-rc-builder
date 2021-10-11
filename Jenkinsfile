pipeline {
    // This is important, because of glibc versions, etc. 
    agent { label 'fedora34' } 
    
    options {
      copyArtifactPermission('OliveTin-integration-tests');
    }
    
    // For the tools we install (eg, buf)
    environment {
      PATH = "/root/go/bin:${env.PATH}"
    }

    stages {
        stage ('Pre-Build') {
            steps {
                git url: 'https://github.com/OliveTin/OliveTin.git', branch: 'main'
                sh 'make grpc'
                sh 'goreleaser release --rm-dist --snapshot'
                
                archiveArtifacts artifacts: 'dist/**', fingerprint: true
                
                //build job: '../OliveTin-integration-tests'
            }
        }
    }
}
