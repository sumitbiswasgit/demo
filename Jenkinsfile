pipeline {
    
    agent any
    
    environment {
        APP_PATH = "my-app"
    }
    
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
        stage ("Generate") {
            steps {
                sh "rm -rf ${APP_PATH}"
                sh "mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false"
            }
        }
        stage ("Build") {
            steps {
                sh "mvn -v"
                sh "mvn -f ${APP_PATH}/pom.xml -DskipTests clean package"
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -f ${APP_PATH}/pom.xml test'
            }
            post {
                always {
                    junit "${APP_PATH}/target/surefire-reports/*.xml"
                }
            }
        }
        stage ("Integration") {
            steps {
                sh "java -cp ${APP_PATH}/target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App"            }
        }
    }
}
