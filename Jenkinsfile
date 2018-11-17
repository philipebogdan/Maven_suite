env.JOB_NAME = env.JOB_NAME.tokenize("/")[0]

pipeline {
  agent {
    label 'master'
  }
      
  stages {
    stage('Build Project1') {
      steps {
        script {
          buildInfo = rtMaven.run pom: 'pom.xml', goals: ' -U clean install -pl env.JOB_NAME -Dmaven.test.skip=true -Dmaven.repo.local=.m2 -Drevision=env.BUILD_NUMBER-SNAPSHOT
		    }
	    }
    }
  }
}
