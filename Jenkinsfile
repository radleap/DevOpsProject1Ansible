pipeline{
    agent any
    stages{
     stage('SCM Checkout') {
      steps{
        git branch: 'main', url: 'https://github.com/radleap/DevOpsAnsible'
            }
        }
     stage('Execute Ansible') {
      steps{
        ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'project_hosts', playbook: 'testplaybook.yml'
            }
        }
 }
}
