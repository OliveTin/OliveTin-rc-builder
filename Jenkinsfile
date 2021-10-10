pipeline {
    agent any

    stages {
        stage ('Pre-Build') {
            steps {
                git url: 'https://github.com/OliveTin/OliveTin.git'
                sh 'goreleaser release --rm-dist --snapshot'
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }
}
