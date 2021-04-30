node {
     stage('___ 통합 단계 ___ 소스 체크') {
         checkout scm
     }

     stage('___ 빌드 단계 ___ 컨테이너 생성') {
         app = docker.build("insobi/front-end")
     }

     stage('___ 빌드 단계 ___ 컨테이너 저장소 전달') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            //  app.push("0.3.12.${env.BUILD_NUMBER}")
            app.push("0.3.12.30")
            app.push("latest")
         }
     }

    stage('___ 배포 단계 ___ 운영환경 배포') {
        kubernetesDeploy(
            configs: 'complete-demo.yaml',
            kubeconfigId: 'K8S_CLUSTER',
            enableConfigSubsitution: true   
        )
    }
}
