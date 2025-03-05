pipeline{
    agent any
    stages{
        stage('SCM Checkout'){
            steps{
                 git branch: 'master', url: 'https://github.com/PradipRandive/maven-project.git'
            }
        }
        stage('maven validate'){
            steps{
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                   sh 'mvn validate'
                }
            }
        }
        stage('maven compile'){
            steps{
                withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                   sh 'mvn compile'
                }
            }
        }
        stage('mvn package'){
          steps{
            withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                   sh 'mvn package'
                }
            }
        }
        stage('deploy the package'){
            steps{
                sshagent(['Tomcat_server']) {
                  sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@10.0.1.13:/usr/share/tomcat/webapps'
                }
            }
        }
    }
}