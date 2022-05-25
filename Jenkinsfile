#!groovy

@Libray('jenkinslib')

def tools = new org.devops.tools()

String workspace = "/opt/jenkins/workspace"
pipeline {
  agent { node {  label "master"
                   customWorkspace "$workspace"
    }
  }
  
    parameters {
    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    }
  
  options {
    timestamps()
    skipDefaultCheckout()
    disableConcurrentBuilds()
    timeout(time: 1, unit: 'HOURS')
  }

  stages {
    stage("GetCode") {
      steps{
        timeout(time:5, unit:"MINUTES"){
            script{
                println('获取代码')
                mvnHome = tool "m2"
                println(mvnHome)
                sh "${mvnHome}/bin/mvn --version"
            }
        }
      }
    }
    stage("Build"){
      steps{
        timeout(time:20, unit:"MINUTES"){
          script{
            println("应用打包")
            println("${PERSON}")
          }
        }
      }
    }
    stage("CodeScan"){
      steps{
        timeout(time:30, unit:"MINUTES"){
          script{
            println("代码扫描")
            tools.PrintMes("this is my lib!")
          }
        }
      }
    }
  }

  post {
    always {
      script{
        println("always")
      }
    }
    success {
      script{
        currentBuild.description += "\n 构建成功！"
      }
    }
    failure {
      script{
        currentBuild.description += "\n 构建失败！"
      }
    }
    aborted {
      script{
        currentBuild.description += "\n 构建取消！"
      }
    }
  }
}
