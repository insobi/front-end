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

    // stage('test') {
    //     withKubeConfig([
    //         credentialsId: 'K8S_CLUSTER',
    //         serverUrl: 'https://refreshday-demo-dns-8851db91.hcp.koreacentral.azmk8s.io:443'
    //     ]) {
    //         sh 'kubectl -n sock-shop delete deployment.apps/front-end'
    //     }
    // }

    stage('운영환경에 컨테이너 배포') {
        kubernetesDeploy(
            configs: 'complete-demo.yaml',
            kubeconfigId: 'K8S_CLUSTER',
            enableConfigSubsitution: true   
        )
    }
}
