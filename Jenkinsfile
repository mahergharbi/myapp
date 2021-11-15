pipeline {

    agent any


    stages {
       stage ('GIT') {
               steps{
                 script{
                     checkout([$class: 'GIT CONNECT', branches: [[name: '*/master']],userRemoteConfigs: [[ credentialsId: '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',url :'https://github.com/mahergharbi/myapp']]])                 
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
