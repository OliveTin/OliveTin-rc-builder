pipeline {
    // This is important, because of glibc versions, etc. 
    agent { label 'fedora34' } 

    stages {
        stage ('Pre-Build') {
            steps {
                git url: 'https://github.com/OliveTin/OliveTin.git', branch: 'main'
                sh 'goreleaser release --rm-dist --snapshot'
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }
}
