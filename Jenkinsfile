currentBuild.displayName = "amazon-#"+currentBuild.number
node
{
    mavenHome = tool name: "maven3.6.3"
stage("SCM Checkout")
{
git branch: 'development', credentialsId: '6d74e282-e235-4b25-9508-a1d4ff8b5b24', url: 'https://github.com/kloudtech-ec-apps/maven-web-application.git'    
}
stage("Build artifact")
{
  sh "${mavenHome}/bin/mvn clean package" 
}
/*stage("Create sonarqube report")
{
  sh "${mavenHome}/bin/mvn sonar:sonar" 
}
stage("Copy artifact into nexus repo")
{
  sh "${mavenHome}/bin/mvn deploy" 
}
stage("Deploy app into tomcat")
{
  sshagent(['9b8fe2c7-8c56-4b29-976e-465c6886c697']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.133.58.3:/opt/tomcat9/webapps/"
}
}*/
stage('SendEmailNotification')
 {
 emailext body: '''Build Finished - Scriptedway

 Regards,
 Hari Jinka,
 9900933955''', subject: 'Build Finshed - Scriptedway', to: 'jinkahariprasad@gmail.com'
 }
}
