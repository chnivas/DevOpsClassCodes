pipeline{
    tools{
        jdk 'myjava'     
        maven 'mymaven'
    }
    agent any
    stages{
        stage('checkout'){
            steps{
               git 'https://github.com/chnivas/DevOpsClassCodes.git'
            }
    }
    stage('compile'){
        steps{
            sh 'mvn compile'
        }
    }
    stage('codeReview'){
        steps{
            sh 'mvn pmd:pmd'
        }
        post{
            always{
                pmd pattern: 'target/pmd.xml'
            }
        }
      }
      stage ('UnitTest'){
          steps{
              sh 'mvn test'
          }
      }
      stage('MetricCheck'){
          steps{
              sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
          }
          post{
              always{
                  cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
              }
          }
      }
      stage ('Packaga'){
          steps{
              sh 'mvn package'
          }
      }
    }
}
