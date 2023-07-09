pipeline {

  agent any

  tools {nodejs "Node.js 18.15.0"}

  stages {
    stage("Clean Up") {
      steps {
        deleteDir()
      }
    }
    stage("Clone") {
      steps {
        sh "git clone https://github.com/alaneicker1975/jenkins-demo.git"
      }
    }
    stage("Install Dependencies"){
      steps {
        dir("jenkins-demo") {
          sh "npm install"
        }
      }
    }
    stage("Test"){
      steps {
        dir("jenkins-demo") {
          sh "npm test"
        }
      }
    }
    stage("Build") {
      steps {
        dir("jenkins-demo") {
          sh "npm run build"
        }
      }
    }
    stage("Deploy"){
      steps {
        dir("jenkins-demo") {
          sh "npm run gh-pages"
        }
      }
    }
  }
}