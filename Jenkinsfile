node{
  stage('git checkout'){
    git credentialsId: 'github', url: 'https://github.com/Jyothiganaparthi/Dockerjen.git'
  }
  stage('maven build'){
    sh 'mvn clean install'
  }
 
}
