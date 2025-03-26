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
     stage('Publish the HTML Reports') {
      steps {
          publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/InsureMe/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                        }
            }
     stage('Docker Image Creation') {
      steps {
           echo 'This is for Docker image build'
           sh 'docker build -t akj200489/insureme:latest .'
            }
          }
     stage('Login to Dockerhub') {
      steps {
             withCredentials([usernamePassword(credentialsId: 'dockeruser', passwordVariable: 'password', usernameVariable: 'username')]) {
          // withCredentials([usernameColonPassword(credentialsId: 'docker-id-user', variable: 'docker-all')]) {
          // withCredentials([string(credentialsId: 'dockercode', variable: 'dockervarcode')]) {
           sh 'docker login -u akj200489 -p ${password}'
                         }
                   }
               }
     stage('Push the Docker image') {
      steps {
        sh 'docker push akj200489/insureme:latest'
                                }
             }
      stage('Ansible Playbook') {
      steps {
        ansiblePlaybook credentialsId: 'sshkey', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'deploy.yml', vaultTmpPath: ''
                                }
                    }  
              }
     
     }
}
