pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/Akshay200k/php-project.git', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t akshayk170/php:v5 .'
                    sh 'docker images'
                }
            }
        }
        stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push akshayk170/php:v5'
                }
            }
        }

        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe221 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe221 -p 8082:80 akshayk170/php:v5'
                    sshagent(['sshkey']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe211 -p 8082:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.231.11 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@13.232.231.11 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
