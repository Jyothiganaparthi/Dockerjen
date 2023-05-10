node{
  stage('git checkout'){
    git credentialsId: 'github', url: 'https://github.com/Jyothiganaparthi/Dockerjen.git'
  }
  stage('maven build'){
    sh 'mvn clean install'
  }
  stage('ssh conncetion'){
    sshagent(['sshid1']) {
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140'
      sh'scp -r /var/lib/jenkins/workspace/pipeline2/* ubuntu@172.31.13.140:/home/ubuntu'
}
  }
  stage('docker build'){
     sshagent(['sshid1']) {
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140 cd /home/ubuntu/'
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140 docker build -t $JOB_NAME:V1.$BUILD_ID .'
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140 docker tag $JOB_NAME:V1.$BUILD_ID jyo425/applicant:v2.$BUILD_ID'
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140 docker tag $JOB_NAME:V1.$BUILD_ID jyo425/applicant:latest'   
  }
 }
 stage('docker push'){
 sshagent(['sshid1']) {
 withCredentials([string(credentialsId: 'dockerid', variable: 'docker')]) {
   sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140 docker login -u jyo425 -p${docker}'
   sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140 docker push jyo425/applicant:v2.$BUILD_ID'
   sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.13.140 docker push jyo425/applicant:latest'
   }
   }
}
  stage('copy files from ansible to mini'){
    sshagent(['mini_id']) {
    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.12.160'
    sh'scp -r /var/lib/jenkins/workspace/pipeline2/* ubuntu@172.31.12.160:/home/ubuntu'
}  
}
}

