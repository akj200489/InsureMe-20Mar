pipeline {
  agent any
   stages {
    stage('Git checkout') {
      steps {
           echo 'This is for cloning the gitrepo'
           git branch: 'main', url: 'https://github.com/akj200489/InsureMe-20Mar.git'
            }
          }
     stage('Maven Package') {
      steps {
           echo 'This is for packaging the application'
           sh 'mvn package'
            }
          }            
     }
}
