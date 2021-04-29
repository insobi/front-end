node {
     stage('소스 다운로드') {
         checkout scm
     }

     stage('소스빌드 및 컨테이너 이미지 생성') {
         app = docker.build("insobi/front-end")
     }

     stage('이미지 저장소에 이미지 업로드') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
             app.push("0.3.12.${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }

    stage('운영환경에 컨테이너 배포') {
        kubernetesDeploy(
            configs: 'complete-demo.yaml',
            kubeconfigId: 'K8S_CLUSTER',
            enableConfigSubsitution: true   
        )
    }
}
