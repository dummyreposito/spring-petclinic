pipeline{
    agent any
    options{
        timeout(time:30, unit: 'MINUTES')
    }
    triggers{
        pollSCM('* * * * *')
    }
    tools{
        jdk 'JDK_17'
        MAVEN 'Maven 3.9.6'
    }
    stages{
        stage('git checkout'){
            steps{
            git branch: 'develop', url: 'https://github.com/dummyreposito/spring-petclinic.git'
            }
        }
      
       
         stage('SonarQube analysis') {
            steps {

                // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
                withSonarQubeEnv('SONAR_Cloud') {
                // requires SonarQube Scanner for Maven 3.2+
                    sh 'mvn clean package sonar:sonar -Dsonar.organization=jenkins-projects -Dsonar.token=ceed9f04368e4216d7ca900c2cb65a08e708e70f -Dsonar.projectKey=jenkins-projects'
                }
            }
        }
        stage('Junit Results'){
            steps{
            junit testResults: '**/target/surefire-reports/TEST-*.xml' 
            }
        }
    }
    }