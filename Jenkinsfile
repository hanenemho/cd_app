pipeline {

    agent any


    stages {
       stage ('GIT') {
               steps{
                 script{
                     checkout([$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs: [[ credentialsId: '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',url :'https://github.com/hanenemho/cd_app']]])                
                 }

}
        }
        stage ('Build') {
               steps{
                 script{
                    sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml -u root --private-key=/var/lib/jenkins/.ssh/id_rsa"
                 }
               }

        }
       
        stage ('Dokcer build') {
               steps{
                 script{
                    sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml -u root --private-key=/var/lib/jenkins/.ssh/id_rsa"
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
