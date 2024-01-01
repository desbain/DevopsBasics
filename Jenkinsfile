pipeline {
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'cloning..'
                // Use withCredentials to provide GitHub credentials
                withCredentials([usernamePassword(credentialsId: 'theitern', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        // Clone the private GitHub repository using the provided credentials
                        git credentialsId: 'theitern', url: "https://github.com/theitern/DevopsBasics.git"
                    }
                }
            }
        }

        stage('Compile') {
            steps {
                echo 'compiling..'
                sh 'mvn compile'
            }
        }

        stage('CodeReview') {
            steps {
                echo 'codeReview'
                sh 'mvn pmd:pmd'
            }
        }

        stage('OWASP Dependency-Check') {
            steps {
                script {
                    def dependencyCheckScan = dependencyCheck publisher: [
                        autoUpdate: true,
                        enableGlobalThreshold: true,
                        failBuildOnCVSS: 8.0,
                        useAuthFile: true,
                        skipOnScmChange: true,
                        skipOnUpstreamChange: true,
                    ]
                }
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
