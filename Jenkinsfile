pipeline{
    agent { label 'SONAR-NODE'}
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps { 
                git url: 'https://github.com/laxmandevopsMarch23/spring-petclinic-pr.git',
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
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'    

            }
        }
    }
    post {
        success {
            mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is success",
                body: "Use this URL ${BUILD_URL} for more info",
                to: 'team-all-qt@qt.com',
                from: 'gottipati423@gmail.com'
        }
        failure {
            mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is failed",
                body: "Use this URL ${BUILD_URL} for more info",
                to: "${GIT_AUTHOR_EMAIL}",
                from: 'gottipati423@gmail.com'
        }
    }

}
