pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                    sh  '''
                        export MAVEN_HOME=/var/jenkins_home/apache-maven/apache-maven-3.8.1
                        export PATH=$PATH:$MAVEN_HOME/bin
                        mvn --version
                        mvn -B -DskipTests clean package
                        '''        
                  }
        }
        stage('Test') {
            steps {
                 sh  '''
                        export MAVEN_HOME=/var/jenkins_home/apache-maven/apache-maven-3.8.1
                        export PATH=$PATH:$MAVEN_HOME/bin
                        mvn --version
                        mvn test
                        '''
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
        stage('Complete'){
            steps{
                echo "Job Complete"
            }
        }
    }
}
