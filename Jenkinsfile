pipeline {

    environment {
        PROJECT = "p02-201504429"
        APP_NAME = "kubeapp"
        CLUSTER = "canary"
        CLUSTER_ZONE = "us-east1-d"
        IMAGE_TAG = "gcr.io/${PROJECT}/app:$APP_VERSION"

    }


    stages {
        stage('build') {
            steps {
                echo "Hola mundo ${IMAGE_TAG}"
            }
        }
    }
}
