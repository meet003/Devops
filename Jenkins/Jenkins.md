
# installation ----------
*Install Jenkins through Docker*
**cmd- docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts**

Note:- -p 50000:50000 is for slave and worker to communtate with each other









pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo "Code cloned"
                // You can use 'git' or any other SCM tool to clone your repository here
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // Build your Docker image
                    sh 'docker build -t your_image_name:latest .'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    // Stop and remove any existing container with the same name
                    sh 'docker stop your_container_name || true'
                    sh 'docker rm your_container_name || true'

                    // Run your Docker container with the newly built image
                    sh 'docker run -d --name your_container_name -p host_port:container_port your_image_name:latest'
                }
            }
        }
    }
}
