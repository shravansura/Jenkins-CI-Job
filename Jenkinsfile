node{
     
    def mavenHome = tool name: "maven 3 8 2"
    
    stage('CodeCheckOut')
    {
        git credentialsId: 'eae12175-15d1-4312-9832-5dcee222462c', url: 'https://github.com/manoj541/Jenkins-CI-Job.git'
    }
    stage('CodeBuild')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('SonarQubeReport')
    {
        sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    stage('UploadArticatintoNexus')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('DeployAppIntoTomcat')
    {
        sshagent(['e81ea2c1-bc18-475b-a14d-3b655fcf6217']){
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.237.136.56:/opt/tomcat9/webapps/" 
    } 
    stage('SendEmailNotification')
    {
        emailext body: '''Deployment is Success

        Regards
        Manoj kumar
        DevOps Team''', subject: 'Deployment is Success', to: 'manojkumar4cs@gmail.com'
    }    
}
}
