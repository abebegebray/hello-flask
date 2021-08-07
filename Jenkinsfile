pipeline{
agent {node {label 'slave'}}
stages{
    stage('Install python3 and pip'){
    steps{
        sh '''
        sudo apt-get install software-properties-common
        sudo add-apt-repository ppa:deadsnakes/ppa
        sudo apt update
        sudo apt install python3
        sudo apt update
        sudo apt install python3-pip
        '''
        }
    }
    stage('Install requires'){
    steps{
        sh 'pip3 install -r requirements.txt '
        }
    }
    stage('Run add-build-num'){
    steps {
            sh 'ls -la'
            sh 'python3 add-build-num.py ${BUILD_NUMBER}'
        }
    }
    stage('Zip files py'){
        steps {
            sh 'tar -zcvf hello-${BUILD_NUMBER}.tar.gz application.py requirements.txt'
        }
    }
}
    post {
        always {
            archiveArtifacts artifacts: '**/*.txt', allowEmptyArchive: true, fingerprint: true, onlyIfSuccessful: true
        }
    }
    
}
