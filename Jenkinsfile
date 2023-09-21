pipeline {
    agent any
    tools{
        maven 'maven_3.8.8'
        jdk 'java_17'
        git 'Default'
    }
    environment{
        WORKSPACE = "${env.WORKSPACE}"
        BRANCH = "${env.BRANCH_NAME}"
    }
    stages {
        stage("check out") {
            steps{
                git branch: "${BRANCH}", credentialsId: '110', url: 'https://github.com/gaidhanishubh/helloworld.git'
            }
        }
        stage("Build"){
            steps{
                sh "mvn clean install"
            }
        }
        stage("Deploy to TOMcat"){
            steps{
                ansiblePlaybook(credentialsId: 'ssh_self_110', playbook: '/ansible/deployon_local.yml', inventory: '/ansible/hosts', extras: "-e work_space=${WORKSPACE}")
            }
        }
    }
}
