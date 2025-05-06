pipeline {
    agent 'monaco'
}

parameter {
    choice(name: 'action', choices: ['deploy', 'update', 'delete'], description: 'Choose an action to perform')
    choice(name: 'env', choices: ['UAT', 'PROD'], description: 'Choose an environment to deploy')
    
}

enviornment {
    UAT {
        environment {
            name = 'UAT'
            DT_URL = 'https://kzo05756.apps.dynatrace.com/'
            DT_API_TOKEN = credentials('DYNATRACE_API_TOKEN')
        }
    }
    PROD {
        environment {
            name = 'PROD'
            DT_URL = 'https://kzo05756.apps.dynatrace.com/'
            DT_API_TOKEN = credentials('DYNATRACE_API_TOKEN')
    }
}



stages {

    stage('Checkout') {
        steps {
            git branch: 'main', url: 'https://github.com/ChandrakantBhagat/monaco.git '
        }
    }
    stage('Deploy') {
        when {
            expression {
                params.action == 'deploy'
            }
        }
        steps {
            script {
                if (params.env == 'UAT') {
                    sh 'monaco deploy --environment UAT --dynatrace-url $DT_URL --dynatrace-api-token $DT_API_TOKEN'
                } else if (params.env == 'PROD') {
                    echo 'Deploying to PROD'
                }
            }
        }
    }
    stage('Update') {
        when {
            expression {
                params.action == 'update'
            }
        }
        steps {
            script {
                if (params.env == 'UAT') {
                    echo 'Updating UAT'
                } else if (params.env == 'PROD') {
                    echo 'Updating PROD'
                }
            }
        }
    }
    stage('Delete') {
        when {
            expression {
                params.action == 'delete'
            }
        }
        steps {
            script {
                if (params.env == 'UAT') {
                    echo 'Deleting UAT'
                } else if (params.env == 'PROD') {
                    echo 'Deleting PROD'
                }
            }
        }
    }
}
}



