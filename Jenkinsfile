pipline{
  agent any
  stages {
    stage('깃 업데이터'){
      steps{
        git url: 'https://github.com/hyoseon-sno/kakaodev.git', branch: 'main'

      }
    }

    stage('도거 이미지 빌드 및 푸시'){
      steps{
        sh '''
        sudo docker build -t brian24/kakaodev:yellow .
        sudo docker push brian24/kakaodev:yellow
        '''
      }
    }

    stage('쿠버네티스 디플로이 서비스'){
      steps{
        sh '''
        ssh 211.183.3.100 'kubectl create deploy deploy-yellow --image=brian24/kakaodev:yellow'
        ssh 211.183.3.100 'kubectl expose deploy deploy-yellow --type=NodePort --port=8004 --target-port=80 --name=deploy-yellow-np'
        '''

      }

  }
}
