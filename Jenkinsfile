pipeline{
    agent any
    stages{
        stage('scm checkout'){
            steps{
                git branch: 'master', url: 'https://github.com/PradipRandive/maven-project.git'
            }
        }
        stage('mvn validate'){
            withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
               sh 'mvn validate'
            }
        }
        stage('mvn compile'){
            withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
               sh 'mvn compile'
            }
        }
        stage('mvn package'){
            withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MAVEN_HOME', mavenSettingsConfig: '', traceability: true) {
                withSonarQubeEnv(credentialsId: 'sonar' , installationName: 'sonar') {
                  sh 'mvn package sonar:sonar'
               }
            }
        }
    }
}