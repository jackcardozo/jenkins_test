pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MVN3"
        jdk "JDK1.8"
    }

    stages {
        stage('PullSCM') {
            steps {
                // Get some code from a GitHub repository
                //git 'https://github.com/jglick/simple-maven-project-with-tests.git'
                git credentialsId: 'github', url: 'https://github.com/jackcardozo/jenkins_test.git'
            }
        }
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true -f api-gateway clean package"                
            }



            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**api-gateway/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'api-gateway/target/*.jar'
                }
            }
        }
    }
}
