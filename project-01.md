## Deploy Application on Tomcat with the help of the S3 bucket.

- first we are closing repo (you can take your repo here) in the master agent.
- then we are building the war file.
- then we are deploying the application on tomcat on master agent.
- then we are copying the war file to s3 bucket (for this please configure the AWS CLI on the server)
- then we are deploying the aplication on the slave agent on tomcat. we are taking the war file here from the s3 bucket.

```
pipeline{
    agent{
        label{
            label 'master'
            customWorkspace "/data/newproject"
        }
    }
    stages{
        stage('clonning repo'){
            steps {
                sh "rm -rf /data/newproject/maven-web-app"
                sh "git clone https://github.com/gk-aws-dev/maven-web-app.git"
            }
        }
        stage ('buil war'){
            steps{
                dir ("/data/newproject/maven-web-app")
                {
                sh "rm -rf /root/.m2/repository"
                sh "mvn clean package"
                }
            }
        }
        stage ('deployment'){
            steps{
                dir ("/data/newproject/maven-web-app/target"){
                sh "cp maven-web-app.war /data/tools/apache-tomcat-9.0.84/webapps"
                }
            }
        }
        stage('copy to s3'){
            steps{
                dir ("/data/newproject/maven-web-app/target"){
                    sh "aws s3 cp maven-web-app.war s3://gkawsdev-bucket"
                }
            }
        }
        stage('deployment on the slave'){
            agent{
                label "JNLP-MVN"
                customWorkspace "/opt/tomcat/apache-tomcat-9.0.85/webapps"
            }
                steps{
                    sh "aws s3 cp s3://gkawsdev-bucket/maven-web-app.war ."
                }
            }
        }
    }
```
