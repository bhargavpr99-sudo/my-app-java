pipeline {
    agent any

    tools {
        maven 'Maven3'   // Name of Maven installation in Jenkins
        jdk 'Java11'     // Name of JDK in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-username/my-java-app.git', branch: 'main'
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

