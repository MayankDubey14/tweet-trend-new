pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
}
    stages {
        stage("build") {
            steps {
                sh 'mvn clean deploy -Dmaven.test.skip=true'  
            }
        }
        
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }

         stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'mayank-sonar-scanner'
            }
            steps{
                withSonarQubeEnv('mayank-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
                   sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
         }     
    
    
    }
}

