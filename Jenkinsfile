  pipeline {
   agent any
   tools {
    maven 'maven3.6.0'
    jdk 'java1.8.0'
   }
   stages {
       
    stage('build') {
     steps {
      sh "mvn -B -DskipTests clean package"
     }
    }
    
    stage('UnitTest') {
     steps {
      sh "mvn test"
     }
     post {
      always {
       junit 'target/surefire-reports/*.xml'
      }
     }
     
    }
    stage('publish') {
     steps {
      sh 'curl -X PUT -u admin:APB4oSbMxjG67dX7gZdt2oPHD4m -T target/spring-boot-first-web-application-git-0.0.1-SNAPSHOT.jar "http://34.221.132.117:8081/artifactory/libs-snapshot/spring-boot-first-web-application-git-0.0.1-SNAPSHOT.jar"'
     }
    }
   stage('Stoping the server') {
       steps {
        sh 'fuser -k 9001/tcp'
       }
      }
    stage('Deploy') {
     steps {
      sh "JENKINS_NODE_COOKIE=do_not_kill_me  nohup java -jar target/spring-boot-first-web-application-git-0.0.1-SNAPSHOT.jar & "
     }
    }
   }
  }
