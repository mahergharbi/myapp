pipeline {

    agent any


    stages {
       stage ('GIT') {
               steps{
                 script{
                     checkout([$class: 'GitSCM', branches: [[name: '*/main']],userRemoteConfigs: [[ credentialsId: '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',url :'https://github.com/hanenemho/MyApp.git']]])                 
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
