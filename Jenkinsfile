pipeline {
    agent any

    tools {
        maven 'Maven3'   // Name of Maven installation in Jenkins
        jdk 'Java11'     // Name of JDK in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/bhargavpr99-sudo/my-app-java.git', branch: 'master', credentialsId: '15439a53-240f-4e5c-803e-3770752e7b8b'

            }
        }

        stage('Build JAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Run Java Program') {
            steps {
                sh 'mvn exec:java -Dexec.mainClass="com.example.App"'
            }
        }

        stage('Build WAR') {
            steps {
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
            echo "✅ Build successful. JAR and WAR archived."
        }
        failure {
            echo "❌ Build failed."
        }
    }
}

