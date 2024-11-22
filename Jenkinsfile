pipeline {
    agent any
    
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M398"
    }

    stages {
        stage('Echo Version') {
            steps {
                sh 'echo "Print Maven Version"'
                sh 'mvn -version'
            }
        }
        stage('Build') {
            steps {
                // Get some code from a Gitea repository
                // git branch: 'main', url: 'https://github.com/rdumitru1/jenkins-hello-world'
                
                // Run Maven Package CMD
                sh "mvn clean package -DskipTests=true"
                archiveArtifacts artifacts: 'target/hello-demo-*.jar', followSymlinks: false
            }
        }
        stage('Unit Test') {
            steps {
                sh "mvn test"
                junit keepProperties: true, keepTestNames: true, stdioRetention: '', testResults: 'target/surefire-reports/TEST-*.xml'
            }
        }
    }
}
