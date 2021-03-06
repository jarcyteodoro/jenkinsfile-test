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
                    echo "##### Building and Executing Unit Tests #####"
                    sh 'mvn clean org.jacoco:jacoco-maven-plugin:0.8.2:prepare-agent test org.jacoco:jacoco-maven-plugin:0.8.2:report install package' 
               }
          }

          stage('Publish JUnit Report') {
               steps {
                    echo "##### Publishing JUnit Report #####"
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
               }
          }

          stage('Upload Artifact/s to Nexus') {
               steps {
                    echo "##### Uploading to Nexus #####"
                    sh label: 'Uploading to Nexus', script: 'curl -v -u admin:admin123 --upload-file target/calculator-unit-test-example-java-1.0.jar http://nexus:8081/repository/maven-releases/Sample-Java-Project/1.0/calculator-unit-test-example-java-1.0.jar'
               }
          }
    }
}
