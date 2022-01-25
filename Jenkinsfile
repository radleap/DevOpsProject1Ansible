pipeline{
    agent any
    stages{
     stage('SCM Checkout') {
      steps{
        git branch: 'main', url: 'https://github.com/radleap/DevOpsProject1Ansible'
            }
        }
     stage('Execute Ansible Install Docker on Ubuntu 1804') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts_testing', playbook: 'docker-install-ubuntu.yml'
            }
        }


     stage('Execute Ansible Simple') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts_testing', playbook: 'testplaybook.yml'
            }
        }

     stage('Execute Ansible Project Main Directive') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts_testing', playbook: 'project_main.yml'
            }
        }
 }
}
