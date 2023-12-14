pipeline{
    agent {label 'JDK-17'}
    options{
        timeout(time:30, unit: 'MINUTES')
    }
    triggers{
        pollSCM('* * * * *')
    }
    tools{
        jdk 'JDK_17'
        maven 'Maven 3.9.6'
    }
    stages{
        stage('git checkout'){
            steps{
            git branch: 'develop', url: 'https://github.com/dummyreposito/spring-petclinic.git'
            }
        }
        stage('build and deploy'){
            steps{
              sh script: 'mvn package' 
            }
        }
        stage('reporting'){
            steps{
            archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar'
            junit testResults: '**/target/surefire-reports/TEST-*.xml' 
            }
        }
    }
}