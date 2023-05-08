node{
  stage('git checkout'){
    git credentialsId: 'github', url: 'https://github.com/Jyothiganaparthi/Dockerjen.git'
  }
  stage('maven build'){
    sh 'mvn clean install'
  }
  stage('ssh conncetion'){
    sshagent(['sshid1']) {
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.7.241'
      sh'scp -r /var/lib/jenkins/workspace/pipeline2/* ubuntu@172.31.7.241:/home/ubuntu'
}
  }
  stage('docker build'){
     sshagent(['sshid1']) {
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.7.241 cd /home/ubuntu/'
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.7.241 docker build -t doc .'
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.7.241 docker tag doc jyo425/applicant:v2.$BUILD_ID'
  }
 }
}
