pipeline {
    agent any
    environment{
        PATH = "/opt/maven/bin:$PATH"
        JAVA_HOME = "/usr/lib/jvm/java-17-openjdk-amd64"
        WORKSPACE = "${env.WORKSPACE}"
        BRANCH = "${env.BRANCH_NAME}"
    }
    stages {
        stage("check out") {
            steps{
                git branch: "${BRANCH}", url: 'https://github.com/gaidhanishubh/helloworld.git'
            }
        }
        stage("Build"){
            steps{
                sh "mvn clean install"
            }
        }
        stage("Deploy to TOMcat"){
            steps{
                ansiblePlaybook inventory: '/ansible/hosts', playbook: '/ansible/deployon_local.yml, extras: '-e work_space=${WORKSPACE}'
            }
        }
    }
}
