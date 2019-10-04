node {
    def mvnHome
    stage('Preparation') {
        echo 'Stage 1 -> Preparation'
        git 'https://github.com/alexpadalka/spring-petclinic.git'
        mvnHome = tool 'Maven'
    }
    stage('Build') {
        echo 'Stage 2 -> Build'
        withEnv(["MVN_HOME=$mvnHome"]) {
            if (isUnix()) {
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
            } else {
                bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
    stage('Results') {
        echo 'Stage 3 -> Results'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
}
