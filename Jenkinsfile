def server = Artifactory.server "LOCAL_ARTI"
def rtMaven = Artifactory.newMavenBuild()
rtMaven.tool = "Maven_3.5.4"
def buildInfo 

pipeline {
  agent {
    label 'master'
  }
      
  stages {
    stage('Build Project1') {
      steps {
        script {
          echo '------------------------------------'

          def baseJobName = env.JOB_NAME.tokenize("/")[0]
          echo "performin clean install + baseJobName 22=============================='${baseJobName}'"

          echo "performin clean install + baseJobName '${baseJobName}'"

          buildInfo = rtMaven.run pom: 'pom.xml', goals: " -U clean install -pl ${baseJobName} -Dmaven.test.skip=true -Dmaven.repo.local=.m2 -Drevision=${env.BUILD_NUMBER}-SNAPSHOT"

        }
	  }
    }
  }
}
