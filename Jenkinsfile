pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'java17'
    }
    stages {
        stage('Download code from GIT') {
            steps {
                git branch: 'main', url: 'https://github.com/utsavasdevops/maven-jenkins6.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('BUILD other project') {
            steps {
                build wait: false, job: 'java-deploy-pipeline'
            }
        }
    }
}
