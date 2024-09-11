pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/KhagendraTiwari/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t khagendratiwari/ktnewimg:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push khagendratiwari/ktnewimg:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 khagendratiwari/ktnewimg:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 khagendratiwari/12septimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.31.19 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.31.19 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
