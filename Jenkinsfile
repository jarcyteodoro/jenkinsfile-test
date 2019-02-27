pipeline {
    agent any
    tools {
    	maven 'MAVEN_DEFAULT'
    }
    stages {
        stage('Build') { 
            steps {
		echo "Building..."
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
