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

			stage('Manual Approval') {
				input 'Lanjutkan ke tahap Deploy?'
			}

			stage('Deploy') {
				sh './jenkins/scripts/deliver.sh'
				sleep 60
			}
        } catch (e) {
            throw e
        } finally {
            junit 'target/surefire-reports/*.xml'
        }
    }
}
