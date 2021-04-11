currentBuild.displayName = "az-#"+currentBuild.number
pipeline{
	//agent any
	agent {
	//label 'slave-1'
	//label 'slave-2'
	label 'nodes'
	}
		
	tools{
	maven 'maven3.6.3'
	}
	triggers{
		pollSCM('* * * * *')
	}
	options{
		//Add the timestamp to the consoleoutput
		timestamps()
		
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '3', daysToKeepStr: '', numToKeepStr: '5')
     
	}
	stages{
		stage("SCM checkout"){
			steps{
				git branch: 'development', credentialsId: '6d74e282-e235-4b25-9508-a1d4ff8b5b24', url: 'https://github.com/kloudtech-ec-apps/maven-web-application.git'
			}
		}
		stage("Build artifact"){
			steps{
				sh "mvn clean package" 
			}
		}
       /* stage("Create sonarqube report"){
			steps{
			sh "mvn sonar:sonar" 
			}
		}
		stage("Copy artifact into nexus repo"){
			steps{
			sh "mvn deploy" 
			}
		}
		stage("Deploy app into tomcat"){
		    steps{
				sshagent(['df356366-2b5c-42fd-8c67-59362bf691b2']){
					sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.19.29.162:/opt/tomcat9/webapps/"
					}
				}
			}
	}*/
	post("Send Email Configuration"){
	success{
	emailext body: '''Build Finished Successfully- DeclarativeWay
	Regards,
	Hari Jinka,
	9900933955''', subject: 'Build Finshed - DeclarativeWay', to: 'jinkahariprasad@gmail.com'
	}
	failure{
	emailext body: '''Build Failed - DeclarativeWayy
	Regards,
	Hari Jinka,
	9900933955''', subject: 'Build Failed - DeclarativeWay', to: 'jinkahariprasad@gmail.com'
	}
  }
}
