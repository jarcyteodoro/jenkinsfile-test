pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
		echo "Building..."
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
