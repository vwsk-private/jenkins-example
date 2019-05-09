pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/prakashk0301/jenkins-example'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'LocalMaven') {
                    sh 'mvn install'
                }
            }
        }

         stage ('deploy to tomcat') {
             
             { sshagent (['deploy-dev']) {
               sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.42.125:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
