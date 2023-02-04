 pipeline {
agent any

tools {
jdk 'java11'
maven 'maven'
       }




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


     

    }

 }

