def containerName="springbootdocker"
def tag="latest"
 
node {
	 
    
  stage('Checkout Source Code') {
    checkout scm
  }

     stage('Maven Clean'){
        sh "mvn clean"
    }

    stage('Maven Install'){
        sh "mvn install"
    }

    

    stage('Image Build'){
        sh "sudo docker build -t $containerName:${env.BUILD_NUMBER} --pull --no-cache ."
        echo "Image build complete"
    }
   
    stage ('Run Application') {
    try {
      // Stop existing Container
       //sh 'docker rm $containerName -f'
      // Start database container here
      sh "sudo docker run -d --name $containerName $containerName:${env.BUILD_NUMBER}"
    } 
	catch (error) {
    } finally {
      // Stop and remove database container here
      
    }
stage('Docker Swarm'){
       sh "sudo docker swarm init"

        sh "sudo docker service create  -p 8082:8083 --name myservice $containerName:${env.BUILD_NUMBER}"
        echo "sudo Docker Swarm Initiated"
    }
  }


  

     
	
 
}
