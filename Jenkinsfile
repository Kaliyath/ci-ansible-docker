pipeline {
    agent any

  //  tools {
        // Install the Maven version configured as "M3" and add it to the path.
 //       maven "M3"
  //  }

    stages {
        stage('scm') {
            steps {
               git credentialsId: 'git-token-root', url: 'git@github.com:Kaliyath/ansible-cd-pipeline.git'
            }
        }
        
        stage('Build') {
            steps {
                
             sh 'mvn clean package'  
            }
        }
        
        stage('ansible') {
            steps {
                
              ansiblePlaybook credentialsId: 'git-token-root', disableHostKeyChecking: true, inventory: 'ansible/dev.inv', playbook: 'ansible/tomcat.yml'
            }
        }
    }
}

