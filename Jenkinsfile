pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B clean package --fail-never' 
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Test report') {
        	steps {
        		sh 'mvn surefire-report:report'
        		sh 'mvn javadoc:javadoc --fail-never'
        	}
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
        }
    }
}
