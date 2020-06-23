// Obtaining an Artifactory server instance defined in Jenkins:
			


pipeline {
     agent { label 'master' }

    stages {
	     stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = D:/satish/MSD/apache-maven-3.6.3/bin:%PATH%"
                    echo "M2_HOME = D:/satish/MSD/apache-maven-3.6.3"
                '''
            }
        }
        stage('Clone sources'){
            steps {
                git url: 'https://github.com/Satishbabu99/pipe.git'
            }
        }

     	stage('SonarQube analysis') {
	     steps {
		//Prepare SonarQube scanner enviornment
		withSonarQubeEnv('SonarQube8.3.1') {
		   bat 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar'
		}
	      }
	}

//	stage('Quality Gate') {
//		steps {
//			timeout(time: 1, unit: 'HOURS') {
			//Parameter indicates wether to set pipeline to UNSTABLE if Quality Gate fails
		        // true = set pipeline to UNSTABLE, false = don't
			// Requires SonarQube Scanner for Jenkins 2.7+
//			waitForQualityGate abortPipeline: false
//		       }
//		 }
//	}

	
	stage('Execute Maven') {
		steps {
		   script {
		
		rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo
			}
		}
		
	}

	
}
}
