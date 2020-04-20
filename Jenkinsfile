node
{
    def mavenHome=tool name: "maven3.6.3"
    
 stage('Checkout')
{
    git branch: 'development', credentialsId: '3a2f3641-9215-496f-bfe2-ce7b7cfd1f30', url: 'https://github.com/devopst2/maven-web-application.git'
}

 stage('Build')
 {
 sh  "${mavenHome}/bin/mvn clean package"
 }
 
 stage('ExecuteSoanrQubeReport')
 {
 sh  "${mavenHome}/bin/mvn sonar:sonar"
 }
 
 stage('UploadArtifactintoNexus')
 {
 sh  "${mavenHome}/bin/mvn deploy"
 }
 
 stage('DeployAppintoTomcat')
 {
     sshagent(['bf16e8f3-91f1-4eb0-966a-ff59e5dadbfa']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war root@13.232.21.19:/opt/apache-tomcat-9.0.33/webapps/"
    }
}
 stage('SendEmailNotification')
{
    emailext body: '''Avengers Assembled


Regards
Thanos''', compressLog: true, subject: 'Avengers Assembled', to: 'devopstest7320@gmail.com'
}
}
