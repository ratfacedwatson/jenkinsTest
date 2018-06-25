

branchName = env.BRANCH_NAME
isPullRequest = branchName.startsWith("PR")
qaEmailId ="fake@west.com"
notifyEmailId = "fake@west.com"


node {
 properties([[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '1', artifactNumToKeepStr: '1', daysToKeepStr: '', numToKeepStr: '']]]);
 deleteDir()
        
	if  (branchName == "Preproduction" ) {
	stage('Checkout') {
        checkout scm
	      repositoryURL = sh(script: 'git config remote.origin.url', returnStdout: true).trim()
	      echo "${repositoryURL}"
	      repositoryName = sh (script: "echo ${repositoryURL} | rev | cut -d '.' -f2 | cut -d '/' -f1 | rev ", returnStdout: true).trim()
              echo "${repositoryName}"
              version = sh (script: 'grep -m1 "/version" pom.xml | awk -F">" \'{print $2}\' | awk -F"<" \'{print $1}\'', returnStdout: true).trim()
              echo "${version}"
	      appName = sh (script: 'grep -m1 "/artifactId" pom.xml | awk -F">" \'{print $2}\' | awk -F"<" \'{print $1}\'', returnStdout: true).trim()
              echo "${appName}"
	      def host = env.BUILD_URL.split('/')[2].split(':')[0]
	      NEW_URL = BUILD_URL.replace(host,"fake.west.com")		                
        }
        stage('Build'){
           withMaven(maven: 'maven-default', jdk: 'jdk-1.8') {
           sh 'mvn clean package'
           }
           }
	}
