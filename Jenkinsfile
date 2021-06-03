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
    tools {
        maven 'maven3'
       // jdk 'jdk8'
    }
    stages{
        stage("Git Checkout"){
            steps{
                echo "========executing Git Checkout========"
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/maheshangalakurthy/clouddevops.git'
            }
        }
        stage('Maven Build'){
            steps{
            echo "=========== Maven Build =============="
            //tool name: 'maven3', type: 'maven'
            sh "mvn package"
            }
        }
        stage("Tomcat Deployment"){
            steps{
               deploy adapters: [tomcat9(credentialsId: 'admintomcat', path: 'manager/html', url: 'http://35.154.15.15:8090/')], contextPath: '/', war: 'target/*.war'        }
        }
    }    
    
    
}
