pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "/usr/bin/mvn compile"
               }
          }
          stage("Unit test") {
               steps {
                    sh "/usr/bin/mvn test"
               }
          }
     
    
stage("Package") {
     steps {
          sh "/usr/bin/mvn package"
     }
}
stage("Docker build") {
     steps {
      
          sh "docker build -t hiral_tomcat ."
     }
}

stage("Deploy to staging") {
     steps {
          sh "docker stop \$(docker ps -qa)"
          sh "docker rm \$(docker ps -qa)"
          sh "docker run -d -it -v /var/lib/jenkins/workspace/docker-war-deployer-project/target/:/usr/local/tomcat/webapps/ -p 8090:8080 --name Testtomcat hiral_tomcat"
     }
}

     }
  post {
     always {
          sh "echo 'I did It'"
     }
}
}
