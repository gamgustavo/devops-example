pipeline {

    agent any
    
    environment {
        PROJECT = "p02-201504429"
        APP_NAME = "kubeapp"
        CLUSTER = "canary"
        CLUSTER_ZONE = "us-east1-d"
        APP_VERSION = 1.0
        IMAGE_TAG = "gcr.io/${PROJECT}/app:$APP_VERSION"
    }


    stages {
        stage('build docker image') {
            steps {
                sh "docker build --build-arg version=${APP_VERSION} -t gcr.io/${PROJECT}/app:${APP_VERSION} ."
            }
        }
        stage('publish docker image') {
            steps {
                sh "gcloud docker -- push gcr.io/$${PROJECT}/app:${APP_VERSION}"
            }
        }        
    }
}
