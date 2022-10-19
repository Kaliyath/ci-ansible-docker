pipeline {
    agent any

  //  tools {
        // Install the Maven version configured as "M3" and add it to the path.
 //       maven "M3"
  //  }

    stages {
        stage('Build') {
            steps {
               git credentialsId: 'git-token', url: 'git@github.com:Kaliyath/springboot-chat-app.git'
            }
        }
        stage('mvn build') {

            steps {

              sh 'mvn -Dmaven.test.failure.ignore=true clean package'

            }

        }

        stage('unit test') {

            steps {

              sh 'mvn test'

              junit '**/target/surefire-reports/*.xml'

            }

        }
        
        stage('checkstyle') {
            steps {
              
              sh 'mvn checkstyle:checkstyle'
              recordIssues(tools: [checkStyle(pattern: '**/checkstyle-result.xml')])
              
            }
        }
        
        stage('sonar') {
            steps {
              
              sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=chat-app \
  -Dsonar.host.url=http://54.244.150.215:9000 \
  -Dsonar.login=sqp_57a5286f794abbc89bfdf450538c0f3523ae6747'
              
            }
        }
        
        stage('nexus') {
            steps {
              
              nexusArtifactUploader artifacts: [[artifactId: 'websocket-demo', classifier: '', file: 'target/websocket-demo-0.0.1-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus-id', groupId: 'websocket-demo', nexusUrl: '44.228.222.42:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '0.0.1-SNAPSHOT'
              
            }
        }
    }
}

