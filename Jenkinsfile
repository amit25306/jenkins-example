pipeline {
    agent any


    stages {
        stage('SCM Checkout'){
          git 'https://github.com/amit25306/jenkins-example'
        }
  }
    {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'Default Maven') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'Default Maven') {
                    sh 'mvn test'
                }
            }
        }


        stage ('install Stage') {
            steps {
                withMaven(maven : 'Default Maven') {
                    sh 'mvn install'
                }
            }
        }

         stage ('deploy to tomcat') {
             steps {
                 sshagent(['tomcat-pipe']) {
                 sh 'scp -o StrictHostKeyChecking=no target/*.jar ec2-user@52.66.152.17:/var/lib/tomcat/webapps/'
      }
             }
   }
}
}
