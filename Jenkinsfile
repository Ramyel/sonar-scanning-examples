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
              sh mvn sonar:sonar \
  -Dsonar.projectKey=teste-sonar-scan \
  -Dsonar.host.url=http://10.200.144.143:9000 \
  -Dsonar.login=23f5b7748c12b32a7946809989849a6e7e1c5495
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
