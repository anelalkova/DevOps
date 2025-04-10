node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("anastasijalalkova/kiii-jenkins")
    }
    if (env.BRANCH_NAME == 'dev') {

        stage('Build image') {
            app = docker.build("anastasijalalkova/kiii-jenkins")
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    } else {
        echo "Branch '${env.BRANCH_NAME}' is not 'dev' — skipping Docker image build and push."
    }
}
