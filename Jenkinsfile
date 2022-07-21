node{
   stage('SCM Checkout'){
       git 'https://github.com/Arefinrumi/pythone-app-repo'
   }
   stage('build Docker Image'){
     sh 'docker build -t arefin007/my-testpython:2.0.1 .'
   }
   stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'dockerpassword1', variable: 'dockerhubpassword')]) {
        sh "docker login -u arefin007 -p ${dockerhubpassword}"
     }
     sh 'docker push arefin007/my-testpython:2.0.1'
   }
   stage('Run Container on Staging'){ 
     def dockerRun = 'docker run  -p 6379:6379 -d --name redis redis'
     def dockerRun1 = 'docker run -p 4040:80 -d --link redis --name my-python-app arefin007/my-testpython:2.0.1'
     def dockerRun2 = 'docker rm -f my-python-app'
     def dockerRun3 = 'docker rm -f redis'
     sshagent(['dockerserver']) {
       sh "ssh -o StrictHostKeyChecking=no -p 2209 root@172.16.18.99 ${dockerRun3}"
       sh "ssh -o StrictHostKeyChecking=no -p 2209 root@172.16.18.99 ${dockerRun2}"
       sh "ssh -o StrictHostKeyChecking=no -p 2209 root@172.16.18.99 ${dockerRun}"
       sh "ssh -o StrictHostKeyChecking=no -p 2209 root@172.16.18.99 ${dockerRun1}"
       sh 'ls'   
     }
   }
}
