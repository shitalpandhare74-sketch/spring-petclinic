pipeline {
    agent any

    environment{
        APP_NAME = "spring_petclinic"
        BUILD_INFO = "Job_Name: ${env.APP_NAME}\nBuild_Number: ${env.BUILD_NUMBER}"
    }

    parameters{
        string(name: 'BRANCH', defaultValue: 'main', description: 'branches to build')
    }

    options{
        timeout(time: 10, unit: 'MINUTES')
        timestamps()
    }

    tools{
        jdk "Java"
        maven "Maven"
    }

    stages{
        stage('Git-Clone'){
            steps{
                git branch: 'main', url: 'https://github.com/your-username/spring-pet-clinic.git'
            }
        }

        stage('Build-package'){
            steps{
                bat 'mvn package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post{
        success{
            mail to: 'shitalpandhare74@gmail.com',
            subject: "SUCCESS: ${APP_NAME}",
            body: """Hello developers,
The Jenkins build has Succeeded
${env.BUILD_URL}
Console logs: ${env.BUILD_URL}console
Artifacts: ${env.BUILD_URL}artifact/target
Regards,
DevOps Team"""
        }

        failure{
            mail to: 'shitalpandhare74@gmail.com',
            subject: "FAILED: ${APP_NAME}",
            body: """Hello developers,
The Jenkins build has Failed
${env.BUILD_URL}
Console logs: ${env.BUILD_URL}console
Please check logs.
Regards,
DevOps Team"""
        }
    }
}
