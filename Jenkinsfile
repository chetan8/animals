pipeline {
    agent any
    environment{
        PATH="/opt/maven-3.8.3/bin:$PATH"
    }
    stages{
        stage('THis is for the stage git'){
            steps{
                echo 'Hi git'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/chetan8/animals.git']]])
            }
        }
        stage('This is for maven'){
            steps{
                echo 'Hello Maven'
                sh 'mvn clean package'
            }
        }
        stage('This is for sonarqube'){
            steps{
                echo 'Hi sonarqube echo'
                withSonarQubeEnv('sonarqube'){
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('This is for tomcat'){
            steps{
                echo 'Hello tomcat'
                deploy adapters: [tomcat8(credentialsId: 'Tomcat_Credentials', path: '', url: 'http://192.168.1.51:8090/')], contextPath: null, war: '**/*.war'
            }
        }
        stage('This is for workspace'){
            steps{
                echo 'Hello workspace'
                cleanWs()
            }
        }
    }
}
