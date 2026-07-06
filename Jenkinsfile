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

        base64File(
            name: 'TEMPLATE_JSON',
            description: 'JSON containing template variables'
        )
    }

    stages {

        stage('Validate Inputs') {
            steps {
                script {
                    if (!params.NAMESPACE?.trim())
                        error("NAMESPACE is required")

                    if (!params.FLOW_ID?.trim())
                        error("FLOW_ID is required")

                    if (!(params.FIRM_ID ==~ /^\d+$/))
                        error("FIRM_ID must be an integer")

                    echo """
                    Namespace : ${params.NAMESPACE}
                    Flow ID   : ${params.FLOW_ID}
                    Firm ID   : ${params.FIRM_ID}
                    Environment: ${params.ENV}
                    """
                }
            }
        }

        stage('Read JSON') {
            steps {
                withFileParameter('TEMPLATE_JSON') {

                    sh '''
                        echo "Uploaded file:"
                        ls -l

                        echo ""
                        echo "Contents:"
                        cat "$TEMPLATE_JSON"
                    '''

                    script {
                        def json = readJSON file: env.TEMPLATE_JSON

                        echo "Parsed JSON:"
                        echo groovy.json.JsonOutput.prettyPrint(
                            groovy.json.JsonOutput.toJson(json)
                        )
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying..."
            }
        }
    }
}
