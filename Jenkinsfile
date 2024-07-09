pipeline {
    agent any
    tools {
        maven 'localMaven'
    }

    parameters {
        string(name: 'tomcat_stag', defaultValue: '35.154.81.229', description: 'Tomcat Staging Server')
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Deploy to Staging Server') {
            steps {
                sh "scp target/*.war jenkins@${params.tomcat_stag}:/usr/share/tomcat/webapps"
            }
        }
    }
}
