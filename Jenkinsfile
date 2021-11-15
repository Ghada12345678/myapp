pipeline {

    agent any


    stages {
       stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[
                            url: 'https://github.com/Ghada12345678/myapp']]])
                }
            }
        }
      stage('Install') {
             steps{
                script{
                    sh "sudo npm install"
                }
            }
        }
        stage ('Build') {
               steps{
                 script{
                    sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml --private-key=/var/lib/jenkins/.ssh/id_rsa -u root"
                 }
               }

        }
       
        stage ('Dokcer build') {
               steps{
                 script{
                    sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml"
                 }
               }

        }


   }
post {
        always {
            cleanWs()
        }
    }
}
