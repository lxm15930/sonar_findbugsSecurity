pipeline {
    agent any
	stages {
	stage('code Analysis'){
	  steps {  
	   script {
	           def sonarHome = tool name:'sonarqubeScanner3.2', type:'hudson.plugins.sonar.SonarRunnerInstallation'
				withSonarQubeEnv('sonarqube'){
				bat "${sonarHome}/bin/sonar-scanner"
				 }
				}
				}
	}
	
	stage('Quality Gate'){
			steps{
				script {
					timeout(time:1,unit:'HOURS'){
					    def qualitygate = waitForQualityGate()
						if (qualitygate.status != "OK") {
						  error "Pipeline aborted due to quality gate coverage failure: ${qualitygate.status}"
						  }
						}
					}
				}
			}
	}
}