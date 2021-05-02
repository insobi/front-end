node {
     stage('소스 체크') {
         checkout scm
     }

     stage('컨테이너 빌드') {
         app = docker.build("insobi/front-end")
     }

     stage('컨테이너 저장소 전달') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            //  app.push("0.3.12.${env.BUILD_NUMBER}")
            app.push("0.3.12.49")
            app.push("latest")
         }
     }

    stage('운영환경 배포') {
        kubernetesDeploy(
            configs: 'complete-demo.yaml',
            kubeconfigId: 'K8S_CLUSTER',
            enableConfigSubsitution: true   
        )
    }
}
