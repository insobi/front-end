node {
     stage('[ Stage #1 ] 소스 체크') {
         checkout scm
     }

     stage('[ Stage #2 ] 소스 빌드') {
         app = docker.build("insobi/front-end")
     }

     stage('[ Stage #3 ] 컨테이너 이미지 생성') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            //  app.push("0.3.12.${env.BUILD_NUMBER}")
            app.push("0.3.12.28")
            app.push("latest")
         }
     }

    stage('[ Stage #4 ] 운영환경 배포') {
        kubernetesDeploy(
            configs: 'complete-demo.yaml',
            kubeconfigId: 'K8S_CLUSTER',
            enableConfigSubsitution: true   
        )
    }
}
