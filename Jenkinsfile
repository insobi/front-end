node {
     stage('Clone repository') {
         checkout scm
     }

     stage('Build image') {
         app = docker.build("insobi/front-end")
     }

     stage('Push image') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
             app.push("0.3.12.${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
}
