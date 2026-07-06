pipeline {
    agent any

    parameters {
        string(
            name: 'NAMESPACE',
            defaultValue: '',
            description: 'Kestra namespace'
        )

        string(
            name: 'FLOW_ID',
            defaultValue: '',
            description: 'Kestra Flow ID'
        )

        string(
            name: 'FIRM_ID',
            defaultValue: '',
            description: 'Firm ID'
        )

        choice(
            name: 'ENV',
            choices: ['qa', 'beta', 'prod'],
            description: 'Deployment environment'
        )

        string(
            name: 'TEMPLATE_JSON',
            description: 'JSON containing template variables'
        )
    }

    stages {
        stage('Read JSON') {
            steps {
                sh '''
                    echo "Uploaded file path:"
                    echo "$TEMPLATE_JSON"

                    echo "Contents:"
                    cat "$TEMPLATE_JSON"
                '''
            }
        }
    }
}
