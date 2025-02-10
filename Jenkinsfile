pipeline {
    agent any

    stages {
        stage('SCM Checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/PradipRandive/pipelines.git'
            }
        }
        stage('complile') {
            steps {
              withMaven(globalMavenSettingsConfig: '', jdk: 'JAVA_HOME', maven: 'MVN_HOME', mavenSettingsConfig: '', traceability: true) {
                  echo 'comilation completed'
}
            }
        }
    }
}
