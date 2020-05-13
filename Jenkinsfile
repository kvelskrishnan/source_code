
node{
  stage ('Build') {
	cleanWs()
    git url: 'https://github.com/pipelineascodecourse/simple_java_project_with_sonarqube'
	
		withMaven(maven: 'maven3_5_2') {
			sh "mvn clean install"
			
			withSonarQubeEnv('MySonarQubeServer'){
				sh "mvn sonar:sonar"
			}				
		} 
	}
}

	

node{
  stage ('Build') {
	cleanWs()
    git url: 'https://github.com/pipelineascodecourse/simple_java_project_with_sonarqube'
	
		withMaven(maven: 'maven3_5_2') {
			sh "mvn clean install"
		} 
		
		withSonarQubeEnv('MySonarQubeServer'){
			sh "mvn sonar:sonar"
		}		
	}

    stage("Quality Gate"){
        timeout(time: 1, unit: 'MINUTES') { 
            def qualityGate = waitForQualityGate()
            if (qualityGate.status != 'OK') {
                error "Pipeline aborted due to quality gate failure: ${qualityGate.status}"
            }
        }
    }
}
