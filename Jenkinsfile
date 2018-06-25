

branchName = env.BRANCH_NAME
isPullRequest = branchName.startsWith("PR")
qaEmailId ="fake@west.com"
notifyEmailId = "fake@west.com"


node {
 properties([[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '1', artifactNumToKeepStr: '1', daysToKeepStr: '', numToKeepStr: '']]]);
 deleteDir()
        
        stage('Build'){
           withMaven(maven: 'maven-default', jdk: 'jdk-1.8') {
           sh 'mvn clean package'
           }
           }
	}
