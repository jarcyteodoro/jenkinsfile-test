pipeline {
     agent any

     tools {
    	     maven 'MAVEN_DEFAULT'
     }
    
     options { timestamps () }

     stages {
          stage('Clean Workspace') {
               steps{
                    deleteDir()
               }
          }

          stage('SCM') {
	          steps {
	               checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'dc343723-8b23-4749-822f-91f0ebfaced6', url: 'https://github.com/jarcyteodoro/sample-java-project.git']]])
	          }
	     }

          stage('Build, JUnit and JaCoCo') { 
               steps {
                    echo "Building..."
                    sh 'mvn clean org.jacoco:jacoco-maven-plugin:0.8.2:prepare-agent test org.jacoco:jacoco-maven-plugin:0.8.2:report install package' 
               }
          }

          stage('Post-build Actions') {
               steps {
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
               }
          }
    }
}
