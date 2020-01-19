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
                sh "yes | gcloud auth configure-docker"
                sh "gcloud docker -- push gcr.io/${PROJECT}/app:${APP_VERSION}"
            }      
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh "export PROJECT_ID=${PROJECT}"
                sh "gcloud config set project ${PROJECT}"
                sh "gcloud config set compute/zone us-east1-d"            
                sh "gcloud container clusters get-credentials ${CLUSTER} --zone ${CLUSTER_ZONE}  --project ${PROJECT}"   
                sh 'sed -i.bak "s#PROJECT_ID#$PROJECT_ID#" app-production.yml'
            }
        }            
    }
}
