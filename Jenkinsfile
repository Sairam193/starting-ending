 pipeline {
agent any

tools {
jdk 'java11'
maven 'maven'
       }


/* environment {
   sonar_url= 'http://172.31.20.136:9000'
   sonar_username= 'admin'
   sonar_password= 'admin'
   nexus_url='172.31.20.136:8081'
   artifact_version='4.0.0'
   imagename = "445194754454.dkr.ecr.us-east-1.amazonaws.com/ram-helloworld"
   registryCredential = 'aws-cred'
   dockerImage = ''



} */



parameters {

string(defaultValue: 'main', description: 'Please type branch name to deploy', name: 'Branch')
}

stages {

     stage('Git Clone') {
         steps { 

                git branch: '${Branch}',
                url: 'https://github.com/Sairam193/starting-ending.git'
             }
         }
    stage('Maven Build') {
        
        steps { 

                sh 'mvn clean install'
             }
         }


      /* stage ('Sonarqube Analysis'){
           steps {
           withSonarQubeEnv('sonarqube') {
           sh '''
           mvn -e -B sonar:sonar -Dsonar.java.source=1.8 -Dsonar.host.url="${sonar_url}" -Dsonar.login="${sonar_username}" -Dsonar.password="${sonar_password}" -Dsonar.sourceEncoding=UTF-8
           '''
 					}
		}
	}

       stage ('Publish Artifact') {
        steps {
          nexusArtifactUploader artifacts: [[artifactId: 'hello-world-war', classifier: '', file: "/var/lib/jenkins/workspace/pipeline1/target/hello-world-war-1.0.0.war", type: 'war']], credentialsId: 'nexus-cred', groupId: 'com.efsavage', nexusUrl: "${nexus_url}", nexusVersion: 'nexus3', protocol: 'http', repository: 'release', version: "${artifact_version}"
         archiveArtifacts '**/*.war'
        }
      }


stage ('Docker Build') {
	steps {
	sh '''
	docker build -t 445194754454.dkr.ecr.us-east-1.amazonaws.com/ram-helloworld:latest --file=Dockerfile ${WORKSPACE} 
	'''
	}
	}
/* 
stage('Docker publish') {                         
    steps {
    script {
        withDockerRegistry(registry:[ credentialsId: 'docker-cred']) {
         sh 'docker push sai6666/helloworld:ram'
       }
       }
      }
     }
*/

 stage('Building image') {
    steps{
      script {
         dockerImage = docker.build imagename
       }
     }
  }
    stage('Deploy Image') {
      steps{
      script {
        docker.withRegistry('http://445194754454.dkr.ecr.us-east-1.amazonaws.com/ram-helloworld:aws-cred')  {
         dockerImage.push("$BUILD_NUMBER")
         dockerImage.push('latest')
        }
       }
      }
   }
      
stage('Remove Unused docker image') {
        steps{
         sh "docker rmi $imagename:$BUILD_NUMBER"
         sh "docker rmi $imagename:latest"
       }
      } */



    }

 }

