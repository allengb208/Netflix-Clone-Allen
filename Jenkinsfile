pipeline {
    agent any
    tools {
        jdk 'jdk17'
        nodejs 'node19'
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout from Git') {
            steps {
                git branch: 'main', url: 'https://github.com/allengb208/Netflix-Clone-Allen.git'
            }
        }
        stage("Sonarqube Analysis") {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh """${SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectName=netflix-clone \
                    -Dsonar.projectKey=netflix-clone """
                }
            }
        }
        stage("quality gate") {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'Sonar-token'
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }
        stage('OWASP FS SCAN') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'NVD-API-KEY', variable: 'NVD-API-KEY')]) {
                        dependencyCheck additionalArguments: '--scan ./ --disableYarnAudit --disableNodeAudit', odcInstallation: 'DP-Check'
                        dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
                    }
                }
            }
        }
        stage("TRIVY FS SCAN") {
            steps {
                sh "trivy fs . > trivyfs.txt"
            }
        }
        stage("Docker Build And Push") {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                        sh " docker build --build-arg TMDB_V3_API_KEY=b3cbca4b4625080fe6949573bf08ff38 -t netflix ."
                        sh " docker tag netflix dockerln008/netflix:latest"
                        sh "docker push dockerln008/netflix:latest"
                    }
                }
            }
        }
        stage('Deploy to container') {
            steps {
                sh 'docker run -d --name Netflix -p 8081:80 dockerln008/netflix:latest'
            }
        }
    }
    post {
        always {
            emailext attachLog: true,
                subject: "'${currentBuild.result}'",
                body: "Project: ${env.JOB_NAME}<br/>" +
                    "Build Number: ${env.BUILD_NUMBER}<br/>" +
                    "URL: ${env.BUILD_URL}<br/>",
                to: 'allengeorge391@gmail.com',                                
                attachmentsPattern: 'trivyfs.txt,trivyimage.txt'
        }
    }
}
