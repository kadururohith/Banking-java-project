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
               sh 'docker build -t kadururohith/project-demo:1 .'
           }
         }
        stage('Login to docker hub and push the file'){
            steps{
                withCredentials([string(credentialsId: 'dockerhubpassword', variable: 'dockerhubpass')]) {
                    sh 'docker login -u kadururohith -p ${dockerhubpass}'
                }
            }
        }
        stage('Push to docker hub'){
          steps{
               sh ' docker push kadururohith/project-demo:1 '
           }
         }
        stage('Deployment stage using ansible'){
          steps{
               ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml', sudoUser: null, vaultTmpPath: ''
           }
         }
        
    }
}
