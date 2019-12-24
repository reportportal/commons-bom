#!groovy

node {

    load "$JENKINS_HOME/jobvars.env"

    stage('Checkout') {
        checkout scm
    }
    stage('Update release version') {
        sh "./mvnw versions:set -DnewVersion=${RELEASE_VERSION} -DgenerateBackupPoms=false"
    }
    stage('Bintray upload') {
        sh "./mvnw -s ${SETTINGS} deploy"
    }
    stage('Push tag') {
        sh "git commit -a -m \'Version update [${RELEASE_VERSION}]\'"
        sh "git tag ${RELEASE_VERSION}"
        sh 'git push --tags'
    }
}
