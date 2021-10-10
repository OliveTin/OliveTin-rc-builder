pipeline {
    // This is important, because of glibc versions, etc. 
    agent { label 'fedora34' } 

    stages {
        stage ('Pre-Build') {
            steps {
                git url: 'https://github.com/OliveTin/OliveTin.git', branch: 'main'
                sh 'go install "github.com/bufbuild/buf/cmd/buf"'
                sh 'go install "github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-grpc-gateway"'
                sh 'go install "github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2"'
                sh 'go install "google.golang.org/grpc/cmd/protoc-gen-go-grpc"'
                sh 'go install "google.golang.org/protobuf/cmd/protoc-gen-go"'
                sh 'buf generate'
                sh 'goreleaser release --rm-dist --snapshot'
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }
}
