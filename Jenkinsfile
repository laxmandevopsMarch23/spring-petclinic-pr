pipeline{
    agent { label 'SONAR-NODE'}
    triggers { pollSCM ('* * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps { 
                git url: 'https://github.com/laxmandevopsMarch23/spring-petclinic-pr.git'
                    branch: 'develop'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar'
                    onlyIfSuccesfull: true
                junit testResults: '**/surefire-reports/TEST-*.xml'    

            }
        }
               

    }

}