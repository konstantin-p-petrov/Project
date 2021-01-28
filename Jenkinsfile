
pipeline {
    agent none
    stages {
        stage('Fetching data from Github!') {
            agent { 
                label 'master'
                 }
            steps {
                checkout scm
                echo '====stage 1: Successfully pulled repo=='
            }
        }
        stage('Packaging of Java Project') {
            agent { 
                label 'master'
                 }
            steps {
                sh 'mvn --version'
                sh 'cd my-app && mvn clean'
                sh 'cd my-app && mvn package'
                echo '====stage 1: Successfully tested and packed Java Web Application===='
            }
        }
        
        stage('Checking Code via Sonar scanner') {
            agent { 
                label 'master'
                 }
            steps {
                script {
                    withSonarQubeEnv("SonarQube") {
                    sh "cd my-app && mvn sonar:sonar -Dsonar.host.url=http://10.240.0.10:9000 -Dsonar.login=26e31db0e12146c1e30d1b5095b6e36a149b77ca"
                    }
                }
            }
        }     


       // stage('Transfering files between OpS and ApS') {
       //     agent { 
       //         label 'test-slave'
       //     }
       //     steps {
       //         sh 'scp jenkins@10.240.0.10:/var/lib/jenkins/workspace/HelloWorld/my-app/target/testing-junit5-mockito-1.0.jar jenkins@10.240.0.20:/home/jenkins'
       //     }
       // }
        stage('Starting Service file') {
            agent { 
                label 'test-slave'
            }
            steps {
                sh 'sudo systemctl stop myapp.service'
                sh 'sudo systemctl start myapp.service'
                sh 'sudo systemctl status myapp.service'
            }
        }
    }
}