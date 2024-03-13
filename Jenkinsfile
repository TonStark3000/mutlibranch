pipeline{
    agent any
    tools{
        maven 'maven-3.9'
    }
    stages{
        stage("SCM Checkout")
        {
            steps{
                git 'https://github.com/javahometech/my-app'
            }
        }
        stage("Maven Build")
        {
         when{
             branch = "Qa"
	 }
		steps{
                sh "mvn clean package"
		sh 'mv target/myweb*war target/myweb.war'

            }
        }
         stage("Deploy to Devtomcat")
        {
            steps{
                sshagent(['Tomcat-1 ']) {
                     sh "scp -o StrictHostKeyChecking=no target/myweb.war  ec2-user@172.31.36.140:/opt/tomcat-9/webapps"

           }
            }
        }
    }
}
