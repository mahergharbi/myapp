pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']],
                        userRemoteConfigs: [[credentialsId: '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',
                            url: 'https://github.com/mahergharbi/myapp']]])
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
	
			steps {
			
			sh "ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml"
	
			}
	}


    stage('Docker') {
               steps{
                script{
                    sh "sudo ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml"
                }
            }
        }


stage('docker_registry') {
    steps{
    script {
        sh "ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml "
          }
       }
    }



      }
}
