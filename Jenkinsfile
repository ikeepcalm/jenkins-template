pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ikeepcalm/jenkins-template', 
                    credentialsId: 'fe534d13-c2fe-4307-85d4-eb474f57f83d', 
                    branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                bat '"C:\\Program Files\\Microsoft Visual Studio\\18\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" "IT Lab 4.vcxproj" /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                bat '"x64\\Release\\IT Lab 4.exe" --gtest_output=xml:test_report.xml'
            }
        }
    }

    post {
        always {
            echo 'Archiving test results...'
            junit testResults: 'test_report.xml', allowEmptyResults: true
        }
    }
}