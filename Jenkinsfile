pipeline {
    agent any   
    parameters {
        choice(name: 'promote', choices: ['SNYPR', 'RIN', 'RIN-Upgrade'], description: 'Promote to:')
        string(name: 'version', defaultValue: '', description: 'Enter the required version')
    }

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws') // Change 'aws' to your actual credential ID
        AWS_SECRET_ACCESS_KEY = credentials('aws') // Change 'aws' to your actual credential ID
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: 'main']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [[$class: 'CleanCheckout'],
                                       [$class: 'CloneOption', noTags: false, shallow: true, timeout: 2],
                                       [$class: 'PruneStaleBranch']],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url:'https://github.com/omeshvalyal/md5_sum_vamshi.git']]])
            }
        }
        stage('Run command') {
            steps {
                sh 'echo "Welcome to Jenkins"'
            }
        }
        stage('Promote the files') {
            steps {
                script {
                   sh """
chmod 775 /var/lib/jenkins/workspace/krishnavamshi/copy.sh
VERSION=${params.version} /var/lib/jenkins/workspace/copy.sh ${params.version}
"""

                }
            }
        }
    }
}
