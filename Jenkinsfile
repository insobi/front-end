node {
     stage('Clone Repo') {
         checkout scm
     }

     stage('Build Image') {
         app = docker.build("insobi/front-end")
     }

     stage('Push Image to Container Registry') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
             app.push("0.3.12.${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }

    stage('Run kubectl') {
        container('kubectl') {
            sh "kubectl apply -f ./complete-demo.yaml"
        }
    }




}
