node{
  stage('git checkout'){
    git credentialsId: 'github', url: 'https://github.com/Jyothiganaparthi/Dockerjen.git'
  }
  stage('maven build'){
    sh 'mvn clean install'
  }
  stage('ansible shh agent'){
    sshagent(['sshid']) {
     sh 'ssh -o StrictHostKeyChecking=no ansible@172.31.7.241
      sh'scp /var/lib/jenkins/workspace/pipeline2 ansible@172.31.7.241:/home/ansible

}
  }
}
