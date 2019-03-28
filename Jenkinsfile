node {

   stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
   stage('Clone Repository') {
        // Get some code from a GitHub repository
        git 'https://github.com/spring-projects/spring-petclinic.git'
    
   }
   
      stage('Open SpringClinic') {
        // Get some code from a GitHub repository
       sh "cd spring-petclinic"
    
   }
   
   
   stage('Build Maven Image') {
    //   sudo docker.build("maven-build")
      sh "./mvnw package"
      
   }
   
   stage('run spring clinic') {
       
   sh " java -jar target/*.jar"

   }
   

}
