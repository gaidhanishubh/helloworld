pipeline {
    agent any
    environment{
        PATH = "/opt/maven/bin:$PATH"
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
        WORKSPACE = "${env.WORKSPACE}"
        BRANCH = "${env.BRANCH_NAME}"
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableConcurrentBuilds()
        timestamps()
        skipDefaultCheckout()
        disableResume()
    }
    triggers {
        pollSCM('H/2 * * * *')
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
                ansiblePlaybook(credentialsId: 'ssh_local_110', playbook: '/ansible/deployon_local.yml', disableHostKeyChecking: true, inventory: '/ansible/hosts', extras: "-e work_space=${WORKSPACE}")
            }
        }
    }
}
