pipeline {
    agent {label "a1"}
    environment { APP_NAME ='complete-prodcution-e2e-pipeline'}
    stages{
        stage('cleanup'){
            steps{
                cleanWs()
            }
        }
        stage('checkout'){
            steps{
                git branch: 'master', url: 'https://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@github.com/techmaverick89/argocd' 
            }
        }
        stage('Update the deployment tags'){
            steps{
                sh """
                cat deployment.yaml
                sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                cat deployment.yaml
                """
            }
        }
        stage('push to github'){
            steps{
                sh """
                    git add .
                    git commit -m "update deployment.yaml"
                    git remote set-url origin https://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@github.com/techmaverick89/argocd.git
                    git push
                """
            }
        }

        ////////////////////////////////
    }
}