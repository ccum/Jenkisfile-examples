pipeline {
    agent {
        docker {
            image 'maven:3-jdk-8' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                echo 'Inciando build'
                sh 'hostname'
                echo 'ingresando en /intave-project'
                sh """cd intave-project && mvn install:install-file -Dfile=../intave-config/lib/ldap2db-bbva/ldap2db-1.0.jar -DpomFile=../intave-config/lib/ldap2db-bbva/ldap2db-1.0.pom && mvn install:install-file -Dfile=../intave-config/lib/ojdbc6/ojdbc6-11.2.0.jar -DpomFile=../intave-config/lib/ojdbc6/ojdbc6-11.2.0.pom && mvn install"""
                echo 'ingresando en /extave-project'
                sh """cd extave-project && mvn install:install-file -Dfile=../intave-config/lib/ldap2db-bbva/ldap2db-1.0.jar -DpomFile=../intave-config/lib/ldap2db-bbva/ldap2db-1.0.pom && mvn install:install-file -Dfile=../intave-config/lib/ojdbc6/ojdbc6-11.2.0.jar -DpomFile=../intave-config/lib/ojdbc6/ojdbc6-11.2.0.pom && mvn install"""
                
            }
        }
    }
    post{
        always{
            echo 'empaquetando'
            archiveArtifacts artifacts: 'intave-project/intave-ear/target/*.ear'
            archiveArtifacts artifacts: 'extave-project/extave-ear/target/*.ear'
        }
    }
}
