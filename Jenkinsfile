node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    // Branch-based conditional logic
    if (env.BRANCH_NAME == 'dev') {

        stage('Build and Push Docker Image') {
            script {
                app = docker.build("anastasijalalkova/kiii-jenkins")

                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                    app.push("${env.BRANCH_NAME}-latest")
                    echo "Docker image pushed for dev branch."
                }
            }
        }

    } else {
        stage('Skip Docker') {
            echo "Branch '${env.BRANCH_NAME}' is not 'dev' — skipping Docker image build and push."
        }
    }
}
