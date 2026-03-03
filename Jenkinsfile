pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/ikeepcalm/jenkins-template', credentialsId: 'fe534d13-c2fe-4307-85d4-eb474f57f83d', branch: 'main' 
            }
        }
        
        stage('Build') {
            steps {
                // Building in Release mode
                bat '"C:\\Program Files\\Microsoft Visual Studio\\18\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Changed path from Debug to Release to match the Build stage above
                bat "x64\\Release\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
        always {
            // Jenkins requires at least one executable step here
            echo 'Archiving test results...'
            
            // This reads the XML file generated in the Test stage
            junit 'test_report.xml'
        }
    }
}