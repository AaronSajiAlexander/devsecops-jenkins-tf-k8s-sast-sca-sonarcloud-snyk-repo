pipeline {
  agent any
  tools { 
        maven 'Maven_3_2_5'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=devsecops-buggyapp -Dsonar.organization=devsecops-buggyapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=1938d5cd7fa0e4ee0a7fb1af8ca1d3ee5cfd4335'
			}
        } 

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
