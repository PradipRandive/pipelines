pipeline{
  agent any
  stages{
    stage('scm checkout'){
      steps{
        git branch: 'master', url: 'https://github.com/PradipRandive/maven-project.git'
      }
    }
    stage('scm validate'){
      steps{
        withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true){
          sh 'mvn validate'
        }
      }
    }
    stage('scm compile'){
      steps{
        withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true){
          sh 'mvn compile'
        }
      }
    }
    stage('scm package'){
      steps{
        withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true){
          sh 'mvn package'
        }
      }
    }
    stage('deploy the code'){
      steps{
        sshagent(['DEvCICD']){
          sh 'scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@10.0.1.15:/usr/share/tomcat/webapps'
        }
      }
    }
  }
}