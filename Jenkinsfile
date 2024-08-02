pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/kadururohith/Banking-java-project/'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with rohith'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with rohith'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa with rohith'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with rohith'){
            steps{
                sh 'mvn package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t myimg .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8091:8091 --name c000 myimg'
            }
        }   
    }
}
