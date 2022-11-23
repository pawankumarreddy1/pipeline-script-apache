pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                sh 'zip -r apache-html-$BUILD_NUMBER.zip . -i *'
                sh 'aws s3 cp apache-html-$BUILD_NUMBER.zip s3://pavanm123/'
            }
        }
        stage('CD') {
            steps {
                sh 'rm -fr *'
                sh 'aws s3 cp s3://pavanm123/apache-html-$BUILD_NUMBER.zip .'
                sh 'unzip apache-html-$BUILD_NUMBER.zip'
                sh 'scp index.html root@10.0.0.177:/var/www/html/'
            }
        }
    }
}
