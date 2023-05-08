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
      sh'scp /var/lib/jenkins/workspace/pipeline2/* ubuntu@172.31.7.241:/home/ubuntu'
}
  }
 
}
