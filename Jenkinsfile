pipeline {
    agent any

    // Use tools configured in Jenkins Global Tool Configuration
    tools {
        maven 'Maven3'   // Make sure this matches the Maven installation name in Jenkins
        jdk 'Java11'     // Make sure this matches the JDK installation name in Jenkins
    }

    environment {
        // Optional: you can define env variables if needed
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/bhargavpr99-sudo/my-app-java.git',
                    branch: 'master',
                    credentialsId: '15439a53-240f-4e5c-803e-3770752e7b8b'  // Replace with your actual credentials ID in Jenkins
            }
        }

        stage('Verify Tools') {
            steps {
                // Debugging step: verify Java & Maven are available
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Run Java Program') {
            steps {
                // Adjust the JAR file name if different
                sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
            }
        }

        stage('Build WAR') {
            steps {
                // This will generate a WAR file if packaging is set up in pom.xml
                sh 'mvn clean package -Dpackaging=war'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar, target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build, run, and archive succeeded!'
        }
        failure {
            echo '❌ Build failed. Check console output for errors.'
        }
    }
}

