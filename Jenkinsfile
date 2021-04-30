node {
     stage('__ 통합 단계 __ 소스 체크') {
         checkout scm
     }

     stage('__ 빌드 단계 __ 컨테이너 생성') {
         app = docker.build("insobi/front-end")
     }

     stage('__ 빌드 단계 __ 컨테이너 저장소 전달') {
         docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            //  app.push("0.3.12.${env.BUILD_NUMBER}")
            app.push("0.3.12.34")
            app.push("latest")
         }
     }

    stage('__ 배포 단계 __ 운영환경 배포') {
        kubernetesDeploy(
            configs: 'complete-demo.yaml',
            kubeconfigId: 'K8S_CLUSTER',
            enableConfigSubsitution: true   
        )
    }
}
