pipeline {
    agent any

    stages {
        stage('Log') {
            steps {
                echo 'checkout and build'
                bat 'java -version'
                bat 'mvn -v'
            }
        }
        stage('Checkout'){
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/manaschaudhary/sonarJenkins.git']]])
            }
        }
        stage('Sonar'){
            steps{
                bat 'mvn sonar:sonar -Dsonar.projectKey=sonar_Jenkins -Dsonar.host.url=http://localhost:9000 -Dsonar.login=a5c3941752785d94ce659007254b7880f77dd572'
            }
        }
        stage('Maven build'){
            steps {
                bat 'mvn clean install -DskipTests'
            }
        }
    }
}