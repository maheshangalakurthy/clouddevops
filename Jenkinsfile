pipeline{
    agent{
        label "master"
    }
    options{
        timestamps()
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    triggers{
        pollSCM('* * * * *')
    }
    stages{
        stage("Git Checkout"){
            steps{
                echo "========executing Git Checkout========"
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/maheshangalakurthy/clouddevops.git'
            }
            post{
                always{
                    echo "========successfully Cloned========"
                }
                success{
                    echo "========successfully Cloned========"
                }
                failure{
                    echo "========Checkout is failed========"
                }
            }
        }

        stage{
            echo "=========== Maven Build =============="
            sh "mvn --version"
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}