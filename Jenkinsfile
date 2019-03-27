import com.nirima.jenkins.plugins.docker.DockerCloud
import com.nirima.jenkins.plugins.docker.DockerTemplate
import com.nirima.jenkins.plugins.docker.DockerTemplateBase
import com.nirima.jenkins.plugins.docker.launcher.AttachedDockerComputerLauncher
import io.jenkins.docker.connector.DockerComputerAttachConnector
import jenkins.model.Jenkins
 
// parameters
def dockerTemplateBaseParameters = [
  bindAllPorts:       false,
  bindPorts:          '',
  cpuShares:          null,
  dnsString:          '',
  dockerCommand:      '',
  environmentsString: '',
  extraHostsString:   '',
  hostname:           '',
  image:              'jenkinsci/slave:latest',
  macAddress:         '',
  memoryLimit:        null,
  memorySwap:         null,
  network:            '',
  privileged:         false,
  pullCredentialsId:  '',
  sharedMemorySize:   null,
  tty:                true,
  volumesFromString:  '',
  volumesString:      ''
]
 
def DockerTemplateParameters = [
  instanceCapStr: '4',
  labelString:    'docker.local.jenkins.slave',
  remoteFs:       ''
]
 
def dockerCloudParameters = [
  connectTimeout:   3,
  containerCapStr:  '4',
  credentialsId:    '',
  dockerHostname:   '',
  name:             'docker.local',
  readTimeout:      60,
  serverUrl:        'unix:///var/run/docker.sock',
  version:          ''
]
 
// https://github.com/jenkinsci/docker-plugin/blob/docker-plugin-1.1.2/src/main/java/com/nirima/jenkins/plugins/docker/DockerTemplateBase.java
DockerTemplateBase dockerTemplateBase = new DockerTemplateBase(
  dockerTemplateBaseParameters.image,
  dockerTemplateBaseParameters.pullCredentialsId,
  dockerTemplateBaseParameters.dnsString,
  dockerTemplateBaseParameters.network,
  dockerTemplateBaseParameters.dockerCommand,
  dockerTemplateBaseParameters.volumesString,
  dockerTemplateBaseParameters.volumesFromString,
  dockerTemplateBaseParameters.environmentsString,
  dockerTemplateBaseParameters.hostname,
  dockerTemplateBaseParameters.memoryLimit,
  dockerTemplateBaseParameters.memorySwap,
  dockerTemplateBaseParameters.cpuShares,
  dockerTemplateBaseParameters.sharedMemorySize,
  dockerTemplateBaseParameters.bindPorts,
  dockerTemplateBaseParameters.bindAllPorts,
  dockerTemplateBaseParameters.privileged,
  dockerTemplateBaseParameters.tty,
  dockerTemplateBaseParameters.macAddress,
  dockerTemplateBaseParameters.extraHostsString
)
 
// https://github.com/jenkinsci/docker-plugin/blob/docker-plugin-1.1.2/src/main/java/com/nirima/jenkins/plugins/docker/DockerTemplate.java
DockerTemplate dockerTemplate = new DockerTemplate(
  dockerTemplateBase,
  new DockerComputerAttachConnector(),
  DockerTemplateParameters.labelString,
  DockerTemplateParameters.remoteFs,
  DockerTemplateParameters.instanceCapStr
)
 
// https://github.com/jenkinsci/docker-plugin/blob/docker-plugin-1.1.2/src/main/java/com/nirima/jenkins/plugins/docker/DockerCloud.java
DockerCloud dockerCloud = new DockerCloud(
  dockerCloudParameters.name,
  [dockerTemplate],
  dockerCloudParameters.serverUrl,
  dockerCloudParameters.containerCapStr,
  dockerCloudParameters.connectTimeout,
  dockerCloudParameters.readTimeout,
  dockerCloudParameters.credentialsId,
  dockerCloudParameters.version,
  dockerCloudParameters.dockerHostname
)
 
// get Jenkins instance
Jenkins jenkins = Jenkins.getInstance()
 
// add cloud configuration to Jenkins
jenkins.clouds.add(dockerCloud)
 
// save current Jenkins state to disk
jenkins.save()


node {
    checkout scm

    def customImage = docker.build("my-image:${env.BUILD_ID}")

    customImage.inside {
        sh 'make test'
    }
 
  stage('Test') {
            steps {
                sh 'node --version'
                 }
  }
 
 stage('Clone Repository') {
        // Get some code from a GitHub repository
  //      git 'https://KristiansK123@bitbucket.org/KristiansK123/spring-petclinic.git'
      git 'https://github.com/spring-projects/spring-petclinic.git'
//      cd spring-petclinic
    
                         }
      
      
}









/*
node {
  
   pipeline {
  
        agent {
        docker {
            image 'maven:3-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    

   stages {
        agent {
        docker { image 'node:7-alpine' }
          }     
      
    
      stage('Test') {
            steps {
                sh 'node --version'
            }
        }
      
      
   stage('Clone Repository') {
        // Get some code from a GitHub repository
  //      git 'https://KristiansK123@bitbucket.org/KristiansK123/spring-petclinic.git'
    ste
      git 'https://github.com/spring-projects/spring-petclinic.git'
//      cd spring-petclinic
    
   }
   
    stage('Test docker ver') {
        // Get some code from a GitHub repository
     // docker version
    sudo systemctl start docker
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
   */
