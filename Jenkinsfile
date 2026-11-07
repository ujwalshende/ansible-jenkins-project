pipeline {   
    agent any
    stages {
        stage("copy files to ansible server"){
            steps{
                script{
                    echo "copying all necessary files to ansible control node"
                    sshagent(['ansible-server-key']){
                        sh "scp -o StrictHostKeyChecking=no ansible/* root@104.248.140.109:/root"

                        withCredentials([sshUserPrivateKey(credentialsId: 'ec2-ansible-server-key', keyFileVariable: 'keyfile', usernameVariable: 'user')]){
                            sh 'scp $keyfile root@104.248.140.109:/root/ssh-key.pem' 
                        }
                    }

                }

            }
        }

    }
      
} 
