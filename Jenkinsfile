
pipeline {
    agent none
    stages {
        stage('Clone gitrepo to Operation Server') {
            agent { 
                node {
                    label 'ops'
                }
            }
            steps {
                echo '====stage 1: SCM Poll Stage===='
                checkout scm
            }
        }
    }

        stage('build') {
            steps {
                agent { 
                node {
                    label 'ops'
                }
            }
                sh 'mvn --version'
               // sh 'mvn compile -f tools/pom.xml -Dlogin.user=ABC -Dlogin.password=ENC(123+w)'
            }
        }
    }
}