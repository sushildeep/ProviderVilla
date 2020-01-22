pipeline {
	agent { label 'WindowsServer' }
	stages {
		stage('Source') { 
			steps {
			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], gitTool: 'default', submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Madhu5555/ProviderVilla.git']]])
			}
		}
		stage('Build') { 
			tools {
				jdk 'java51'
				maven 'maven51'
			}
			steps {
				powershell 'mvn clean package'
				
			}
		}
		
		stage('Code Quality') {
                   steps {
					script{
						withSonarQubeEnv(installationName: 'qa'){
						bat label: '', script: 'mvn sonar:sonar'
                         }
                       }
		   }
		
		}
		}
		}
