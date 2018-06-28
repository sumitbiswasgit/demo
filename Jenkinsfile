pipeline {
    
    agent any
    
    tools {
        maven 'maven-3.5.0'
        jdk 'jdk1.8.0_121'
    }
    
    stages {
        stage ("Initialize") {
            steps {
                sh '''
                echo "PATH = ${PATH}"
                echo "JAVA_HOME = ${JAVA_HOME}"
                echo "MAVEN_HOME = ${MAVEN_HOME}"
                '''
            }
        }
        stage ("Build") {
            steps {
                sh "mvn -v"
                sh "mvn -B -DskipTests clean package"
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
