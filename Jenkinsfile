


node {
    def app
    environment {
        PROJECT = "p02-201504429"
        APP_NAME = "kubeapp"
        CLUSTER = "canary"
        CLUSTER_ZONE = "us-east1-d"
        APP_VERSION = 1.0
        IMAGE_TAG = "gcr.io/${PROJECT}/app:$APP_VERSION"
    }    

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("gustavogamboa/devopsapp:1.0")
    }

    stage('Test image') {        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'DockerHub02') {
            app.push("1.0")            
            } 
            echo "Trying to Push Docker Build to DockerHub"
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "ks8/lb/app-lb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

}