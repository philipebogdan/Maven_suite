
    // Get Artifactory server instance, defined in the Artifactory Plugin administration page.
    def server = Artifactory.server "LOCAL_ARTI"
    // Create an Artifactory Maven instance.
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo 
    def baseJobName = env.JOB_NAME.tokenize("/")[0]
    def thisJob = baseJobName.trim()
pipeline {
  agent {
    label 'master'
  }
      
  stages {
    stage('Build Project1') {
      steps {
        script {
          // Tool name from Jenkins configuration
          rtMaven.tool = "Maven_3.5.4"
          // Set Artifactory repositories for dependencies resolution and artifacts deployment.
          rtMaven.deployer releaseRepo:'libs-release-local', snapshotRepo:'libs-snapshot-local', server: server
          rtMaven.resolver releaseRepo:'libs-release', snapshotRepo:'libs-snapshot', server: server    
            
          //def baseJobName = env.JOB_NAME.tokenize("/")[0].trim()
	      println "This is the Job name: " + baseJobName
          buildInfo = rtMaven.run pom: 'pom.xml', goals: " -U clean install -pl ${baseJobName} -Dmaven.test.skip=true -Dmaven.repo.local=.m2 -Drevision=env.BUILD_NUMBER-SNAPSHOT"
		}
	  }
    }
  }
}
