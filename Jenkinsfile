pipeline {

    agent any

    tools { nodejs "nodejs" }

    environment {
        // Define environment variables used throughout the pipeline
        serverIp = "192.168.200.155"                    // Replace with your server's IP address
        serverUser = "YOUR_SERVER_USERNAME"            // Replace with your server's username
    }

    stages {

        stage('Checkout') {
            steps {
                // Checkout the code from your Git repository
                git 'https://github.com/Prabhatkumar-3/React-app-Dep.git'
            }
        }

        stage('Build React App') {
            steps {
                // Install project dependencies and build the React application
                sh 'npm install'
                sh 'npm run build'
            }
        }

      
        stage('Deploy to Server Server') {
            steps {
      
                    // SSH into the server and execute Docker container management and deployment commands
                    sshagent(['kubernetes-master']) {
                        sh returnStatus: true, script: "ssh -o StrictHostKeyChecking=no ${serverUser}@${serverIp} ${stopcontainer} "
                        sh returnStatus: true, script: "ssh -o StrictHostKeyChecking=no ${serverUser}@${serverIp} ${delcontName}"
                        sh returnStatus: true, script: "ssh -o StrictHostKeyChecking=no ${serverUser}@${serverIp} ${delimages}"

                        // Start a Docker container on the server
                        sh "ssh -o StrictHostKeyChecking=no ${serverUser}@${serverIp} ${drun}"
                    }
                }
            }
        }
    }
}
