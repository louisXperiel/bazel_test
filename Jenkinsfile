pipeline {
    agent {
        docker {
            image 'insready/bazel'
            args '-v "$PWD":/usr/src/app'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [[$class: 'CleanCheckout']],
                    submoduleCfg: [],
                    userRemoteConfigs: [[credentialsId: 'xperiel', url: 'https://github.com/Xperiel/Master.git']]
                ])
            }
        }
        stage('Bazel') {
            steps {
                sh 'bazel --batch --output_base=/bazel-output/apiintegration-ios-build run src/main/java/com/xperiel/devtools/ci/projects:apiintegration-ios-build'
            }
        }
        
    }
}