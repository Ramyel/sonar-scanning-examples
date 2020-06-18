pipeline {
    agent any

    stages {
        stage('Getting code from SCM') {
            steps {
            git 'https://github.com/Ramyel/sonar-scanning-examples.git'
              echo 'Building..'
            }
        }
        stage('Sonar Analysis') {
            steps {
            script{
              withSonarQubeEnv('sonarserver'){
              sh '''
              mvn clean package -DskipTests && 
                            ${SONAR_HOME}/bin/sonar-scanner -Dproject.settings=sonar-project.properties
              '''
                }
                timeout (time:1, unit: 'HOURS'){
                def qg = waitForQualityGate()
                if (qg.status != 'OK')
                error "Pipeline Aborted: ${qg.status}"
                }
            }
            }
        }
     }
}
