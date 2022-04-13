pipeline {
    agent {
        kubernetes {
            defaultContainer 'worker'
            inheritFrom 'cki-worker'
        }
    }
    options {
        timestamps()
    }
    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }
        stage('Init') {
            steps {
                dir("stacks/create-stack") {
                    sh "go run . --build-destination=europe-west3-docker.pkg.dev/sap-se-gcp-istio-dev/focal/build-image --run-destination=europe-west3-docker.pkg.dev/sap-se-gcp-istio-dev/focal/run-image --stack=base --stacks-dir=.. --version=0.0.1 --publish"
                }
            }
        }
    }
}