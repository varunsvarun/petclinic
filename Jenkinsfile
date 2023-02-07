pipeline {
    agent any
    stages {
        stage('git_clone'){
            steps{
                git branch: 'main', credentialsId: '473e670a-92bd-4ea2-90d2-7bf5373e3cf4', url: 'https://github.com/vsk2408/spring-petclinic-docker.git'
            }
        }
        stage('build'){
           steps{
               sh 'mvn clean install -X -U'
           }
       }
       stage('docker_build'){
          steps{
              sh 'docker build -t petclinic-app -f Dockerfile .'
              sh 'docker save -o petclinic-app.tar petclinic-app:latest'
              sh 'chown jenkins:jenkins petclinic-app.tar'
          }
       }
       stage('ansible_playbook'){
           steps{
               sh ''' chmod +X ansible.yaml
                     ansible-playbook -i /etc/ansible/inv ansible.yaml'''
           }
       }
    }
}    
