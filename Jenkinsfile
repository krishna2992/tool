pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Show Template Information') {
            steps {
                sh '''
                    python3 script.py \
                        describe \
                        templates/workflow.yaml
                '''
            }
        }

        stage('Upload Configuration') {
            steps {
                script {

                    def uploaded = input(
                        message: 'Upload deployment configuration JSON',
                        ok: 'Continue',
                        parameters: [
                            base64File(
                                name: 'CONFIG_JSON',
                                description: 'Upload config.json'
                            )
                        ]
                    )

                    withFileParameter('CONFIG_JSON') {
                        sh '''
                            cp "$CONFIG_JSON" config.json
                        '''
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    python3 script.py \
                        deploy \
                        templates/workflow.yaml \
                        config.json
                '''
            }
        }
    }
}
