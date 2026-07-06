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

        file(
            name: 'TEMPLATE_JSON',
            description: 'JSON containing template variables'
        )
    }

    stages {
        stage('Run Python') {
            steps {
                sh '''
                    echo "JSON file: $TEMPLATE_JSON"

                    python3 script.py \
                        --json "$TEMPLATE_JSON"
                '''
            }
        }
    }
}
