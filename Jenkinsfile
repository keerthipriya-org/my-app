@Library('pipeline-library-demo')_
pipeline {
    agent {label 'maven-label'}

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3.8.4"
    }

    stages {
        stage('Build') {
            steps {
         cleanWs()
                SayHello('Jenkins')
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/keerthipriya-org/my-app.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
