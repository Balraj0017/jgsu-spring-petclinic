pipeline {
    agent any
    tools {
        maven 'Maven 3.8.4'
        jdk 'jdk11'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                   cd spring-petclinic
                   ./mvnw package
                '''
            }
        }

        stage ('Build') {
            steps {
                sh 'java -jar target/*.jar --server.port=8081' 
            }
           
        }
           stage ('Docker') {
            steps {
                sh 'docker run -e MYSQL_USER=petclinic -e MYSQL_PASSWORD=petclinic -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=petclinic -p 3306:3306 mysql:5.7.8' 
            }
           
        }
         stage ('Database-connection') {
            steps {
                sh ' mvn spring-boot:run -Dspring-boot.run.profiles=mysql' 
            }
           
        }
    }
}
