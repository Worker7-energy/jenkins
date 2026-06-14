pipeline {
    agent any
    parameters {
        string(name: 'ENV', defaultValue: 'dev', description: 'Target environment')
    }
    stages {
        stage('Deploy') {
            steps {
                echo "Deploying to ${params.ENV}"
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'MyServer',
                            transfers: [
                                [
                                    sourceFiles: '**/*',
                                    excludes: 'Jenkinsfile',
                                    removePrefix: '',
                                    remoteDirectory: "/var/www/app-${params.ENV}",
                                    flatten: false,
                                    cleanRemote: false
                                ]
                            ],
                            usePromotionTimestamp: false,
                            useWorkspaceInPromotion: false,
                            verbose: false
                        )
                    ]
                )
            }
        }
        stage('Cleanup') {
            steps {
                cleanWs()
            }
        }
    }
}
