pipeline {
    agent {label 'maven'}

environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}

    stages {
        stage ("build") {
            steps {
                sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
        }

        stage ("test"){
            steps {
                sh 'mvn surefire-report:report'
            }
        }

        stage ("SonarQube analysis"){
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }

}