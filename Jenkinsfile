node {


   stage('Clone Repository') {
      // Get some code from a GitHub repository
      sh 'rm -r spring-petclinic'
        // Get some code from a GitHub repository
        sh 'git clone https://github.com/spring-projects/spring-petclinic'
    
   }
   
   /*
   
      stage('Open SpringClinic') {
        // Get some code from a GitHub repository
       sh "cd spring-petclinic"
    
   }
   */
   
   stage('Build Maven Image') {
    //   sudo docker.build("maven-build")
      sh "./mvnw package"
      
   }
   
   stage('run spring clinic') {
       
   sh " java -jar target/*.jar"

   }
   

}
