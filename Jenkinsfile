pipeline {
    agent any

    environment {
        MSBUILD = "C:\\Program Files\\Microsoft Visual Studio\\18\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe"
    }

    stages {        
        stage('Build') {
            steps {
                bat "\"${MSBUILD}\" \"IT Lab 4.vcxproj\" /t:Build /p:Configuration=Release"
            }
        }

        stage('Test') {
            steps {
                // Path updated based on your successful build log
                bat '"Release\\IT Lab 4.exe" --gtest_output=xml:test_report.xml'
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