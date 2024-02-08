<<<<<<< HEAD
pipeline{
tools{
jdk 'myjava'
maven 'mymaven'
}
agent any
stages{
stage('Clone Repo')
{
steps{
git 'https://github.com/desbain/DevopsBasics.git'
}
}
stage('Compile the code')
{
steps{
sh 'mvn compile'
}
}
stage('Code Analysis')
{
steps{
sh 'mvn pmd:pmd'
}
}
stage('code coverage')
{
steps{
sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
}
}
stage('Build the artifact')
{
steps{
sh 'mvn package'
}
}
}
}
=======
        pipeline{
            tools{
                jdk 'myjava'
                maven 'mymaven'
            }
            agent none
            stages{
                stage('Checkout'){
                    agent any
                    steps{
                echo 'cloning...'
                        git 'https://github.com/desbain/devops-basics.git'
                    }
                }
                stage('Compile'){
                    agent {label 'Master'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview'){
                    agent {label 'Slave_1'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest'){
                    agent {label 'Slave_1'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package'){
                    agent any
                    steps{
                        sh 'mvn package'
                    }
                }
            }
        }
>>>>>>> 45eb9ba61459da7861f5ae4534e27a9b22138853
