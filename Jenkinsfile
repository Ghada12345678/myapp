pipeline {

    agent any


    stages {
       stage ('GIT') {
               steps{
                 script{
                     checkout([$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs: [[ credentialsId: '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',url :'https://github.com/Ghada12345678/myapp']]])                
                 }

}
        }
        stage ('Build') {
               steps{
                 script{
                    sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml"
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
