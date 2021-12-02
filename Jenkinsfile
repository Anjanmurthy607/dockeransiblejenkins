pipeline{
    agent any
    tools {
      maven 'maven3'
    }
    environment {
      DOCKER_TAG = getVersion()
    }
    stages{
        stage('SCM'){
            steps{
                git credentialsId: 'github', 
                    url: 'https://github.com/javahometech/dockeransiblejenkins'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
    
        
        stage('Docker Deploy'){
            steps{
              sh "scp -o StrictHostKeyChecking=no Dockerfile ansadmin@172.31.1.104:/home/ansadmin"
	          sh "scp -o StrictHostKeyChecking=no deploy-docker.yml ansadmin@172.31.1.104:/home/ansadmin"
	          sh "scp -o StrictHostKeyChecking=no ansadmin@172.31.1.104:/home/ansadmin -C \"sudo ansible-playbook deploy-docker.yml\""
            }
        }
    }
}

