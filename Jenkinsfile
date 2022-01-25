pipeline{
    agent any
    stages{
     stage('SCM Checkout') {
      steps{
        git branch: 'main', url: 'https://github.com/radleap/DevOpsProject1Ansible'
            }
        }

     stage('Testing: Ansible Install Docker on EC2 Ubuntu 1804') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts_testing', playbook: 'playnook-docker-install-ubuntu.yml'
            }
        }

     stage('Testing: Ansible Build Container and Website') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts_testing', playbook: 'playbook-deploy.yml'
            }
      post{ failure {error "Failed to create testing website."}
            unstable {error "Unstable, failed to create testing website."}
           }
        }

     stage('Production: Ansible Install Docker on EC2 Ubuntu 1804') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts_prod', playbook: 'playbook-docker-install-ubuntu.yml'
            }
        }

     stage('Production: Ansible Build Container and Website') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts_prod', playbook: 'playbook-deploy.yml'
            }
        }

 }
}
