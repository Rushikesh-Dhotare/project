pipeline {
    agent any

    

    stages {

        
        stage('clean-mvn-package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('rds-setup') {
            steps {
                sh '''
            cd target
            unzip LoginWebApp.war
            sed -i 's|localhost|database-1.c1acecagmatm.ap-south-1.rds.amazonaws.com|g' userRegistration.jsp
            sed -i 's|"root", "root"|"admin", "rushi12345"|g' userRegistration.jsp
            rm -f LoginWebApp.war
            zip -r LoginWebApp.war *
                '''
            }
        }

        stage('deploy') {
            steps {
                sh 'cp target/LoginWebApp.war ~/servers/apache-tomcat-10.1.49/webapps/'
            }
        }
    }
}
