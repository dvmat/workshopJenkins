pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Compileaza') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Ruleaza teste') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Creaza artefacte') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
