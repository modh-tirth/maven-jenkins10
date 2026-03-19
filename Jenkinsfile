pipeline {
    agent any
    tools {
        maven 'maven1'
        jdk 'java1'
    }
    stages {
        stage('Download') {
            steps {
                echo "downloading the code"
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/modh-tirth/maven-jenkins10.git']])
            }
        }
        stage('build') {
            steps {
                echo "building the code"
                sh 'mvn clean package'
            }
        }
        stage('copy artifact') {
            steps {
                echo "copying the artifact"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('build other job') {
            steps {
                echo "building other job"
                build wait: false, job: 'depoly-pipline'
            }
        }
    }
}
