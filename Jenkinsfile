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
                    sh 'docker build -t akshayk170/php:v1 .'
                    sh 'docker images'
                }
            }
        }
        stage('Docker login') {
    steps {
        withCredentials([usernamePassword(credentialsId: 'doc_cred', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
            // Encode the password using base64
            def encodedPassword = sh(script: "echo -n $PASS | base64", returnStdout: true).trim()

            // Login to Docker registry using the encoded password
            sh "echo \"$encodedPassword\" | docker login -u $USER --password-stdin"

            // Continue with other Docker-related steps
            sh 'docker push akshayk170/php:v1'
        }
    }
}

        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe221 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe221 -p 8082:80 akshu20791/2febimg:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe211 -p 8082:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.93.252 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.93.252 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
