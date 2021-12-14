pipeline {
  agent {
    docker {
      image 'maven:3.8.1-adoptopenjdk-11'
      args '-v /root/.m2:/root/.m2'
    }
  }

 options {
        skipStagesAfterUnstable()
   }


  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }
    stage('Test') {
          steps {
            sh 'mvn test'
        }
    stage('Deliver')  {
          steps {
             sh './jenkins/scripts/deliver.sh'
        }

     }           
        post {
             always {
                 junit 'target/surefire-reports/*.xml' //3
             }
         }
     }

   }
}
