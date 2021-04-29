node {
     stage('Clone repository') {
         checkout scm
     }

     stage('Build image') {
         app = docker.build("insobi/front-end:0.3.12.2")
     }
}
