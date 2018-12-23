pipeline{
    agent any
    tools {
        jdk 'Java8'
    }
    stages{
        stage('Checkout'){
            steps {
            echo "Checkout"
            deleteDir()
            checkout([$class: 'GitSCM', branches: [[name: "*/${params.BRANCH}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'c9e971bc-0248-4948-a89b-9c130ff40259', url: 'https://github.com/Madugula001/simple-app.git']]])


            }
        }
        stage('Build'){
            steps{
                echo "Build"  
                bat 'dir'
                bat "mvn clean package"
            }
        }
        stage('Test'){
            steps{
            echo "mvn clean test"
            }
        }
        stage('Variables'){
            steps{
                bat "java -version"
            }
        }
        /*
        stage('CODE COVERAGE') {
          steps {
              //dir('MarketRiskDataService/r3-rest-service'){
            script {
              try {
                jacoco changeBuildStatus: true, minimumBranchCoverage: '20', minimumClassCoverage: '45', minimumInstructionCoverage: '32', minimumLineCoverage: '39', minimumMethodCoverage: '54'
                } catch (e) {
                  currentBuild.result = 'ABORTED'
                  throw e
                }
              }
           // }
            }
            post {
              failure {
                //bat 'return'
                echo "Failed"
                //emailext attachLog: true, body: 'JACOCO CODE COVERAGE has failed ', subject: 'FAILED', to: "${Emaild}"
              }
    
            }
          }*/
        stage('SonarQube'){
            steps{
             //bat "mvn -Dhttps.protocols=TLSv1.2 sonar:sonar -Dproject.settings=sonar-project.properties -Dsonar.sources=."
              bat "mvn  clean package sonar:sonar -Dsonar.projectKey=XYZ -Dsonar.porjectName=Soundar -Dmaven.test.skip=true"
            }
        }
    }
}
