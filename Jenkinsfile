node {
    checkout scm
    docker.image('maven:3.9.2-eclipse-temurin-17').inside {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }
        try {
            stage('Test'){
                sh 'mvn test'
            }
        } catch (e) {
            throw e
        } finally {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
