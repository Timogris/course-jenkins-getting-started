pipeline {
    agent any
    // triggers {
    //     pollSCM('* * * * *')
    // }
    stages {
        stage('Checkout') {
            steps {
            git branch: 'main', url: 'https://github.com/Timogris/jgsu-spring-petclinic.git'
            }
        }
        
        stage('Build') {
            steps {
            sh './mvnw clean package'
            }
        

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                // }
                // changed {
                    emailext subject: 'Job \'${JOB_NAME}\' (${BUILD_NUMBER}) is waiting for input',
                        body: 'Please go to ${BUILD_URL} and verify the build',
                        attachLog: true,
                        compressLog: true,
                        to: "test@jenkins",
                        recipientProviders: [upstreamDevelopers(), requestor()],
                }
            }
        }
    }
}

