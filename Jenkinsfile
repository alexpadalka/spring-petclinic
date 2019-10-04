node {
    stage('Preparation') {
        git 'https://github.com/alexpadalka/spring-petclinic.git'
        echo 'Stage 1 -> Preparation'
    }
    stage('Build') {
        echo 'Stage 2 -> Build'
        if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
        } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
        }
    }
    stage('Results') {
        echo 'Stage 3 -> Results'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
}
