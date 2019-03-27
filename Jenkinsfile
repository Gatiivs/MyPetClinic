
node {

   pipeline {
    agent {
        docker { image 'node:7-alpine' }
          }
    stages {
        stage('Test') {
            steps {
                sh 'node --version'
                  }
                      }
           }
}
   
   
   
   stage('Clone Repository') {
        // Get some code from a GitHub repository
  //      git 'https://KristiansK123@bitbucket.org/KristiansK123/spring-petclinic.git'
      git 'https://github.com/spring-projects/spring-petclinic.git'
//      cd spring-petclinic
    
   }
   
    stage('Test docker ver') {
        // Get some code from a GitHub repository
      docker version
    
   }
   
   
   stage('Build Maven Image') {
       docker.build("maven-build")
   //   ./mvnw package
      
   }
   
   

   stage('Run Maven Container') {
       
        //Remove maven-build-container if it exisits
        sh " docker rm -f maven-build-container"
        
        //Run maven image
        sh "docker run --rm --name maven-build-container maven-build"
   }
   
   stage('Deploy Spring Boot Application') {
        
         //Remove maven-build-container if it exisits
        sh " docker rm -f java-deploy-container"
       // denisdbell in next line, but unsure what should i redirect it to
        sh "docker run --name java-deploy-container --volumes-from maven-build-container -d -p 8080:8080 denisdbell/petclinic-deploy"
   }

}
