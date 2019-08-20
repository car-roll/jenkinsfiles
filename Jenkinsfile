@Library('github.com/triologygmbh/jenkinsfile@9b-shared-library') _

node('docker') {
    catchError {

        stage('Checkout') {
            checkout scm
        }

        stage('Build') {
            mvn 'clean install -DskipTests'
        }

        stage('Unit Test') {
            mvn 'test'
        }
    }

    // Archive Unit and integration test results, if any
    junit allowEmptyResults: true,
            testResults: '**/target/surefire-reports/TEST-*.xml, **/target/failsafe-reports/*.xml'

    //mailIfStatusChanged env.EMAIL_RECIPIENTS
}
