pipeline {

  agent any

  tools {nodejs "Node.js 18.15.0"}

  parameters {
    booleanParam(defaultValue: true, description: "Enable Service?", name: "myBoolean")
    choice(choices: ["TEST","DEV","QA","PREPROD","PROD"], description: "Which environment to deploy to?", name: "deployEnv")
  }

  stages {
    stage("Cleanup") {
      steps {
        deleteDir()
      }
    }
    stage("Build Info") {
      steps {
        echo "********** Checking Params **********"
        echo "BooleanParam set to: ${params.myBoolean}"
      }
    }
    stage("Clone") {
      steps {
        echo "********** Cloning Repo **********"
        sh "git clone https://github.com/alaneicker1975/jenkins-demo.git"
      }
    }
    stage("Install"){
      steps {
        dir("jenkins-demo") {
          echo "********** Installing Dependencies **********"
          sh "npm install"
        }
      }
    }
    stage("Test"){
      steps {
        dir("jenkins-demo") {
          echo "********** Running Tests **********"
          sh "npm test"
        }
      }
    }
    stage("Build") {
      steps {
        dir("jenkins-demo") {
          echo "********** Building **********"
          sh "npm run build"
        }
      }
    }
    // stage("Deploy"){
    //   steps {
    //     dir("jenkins-demo") {
    //       echo "********** Deploying **********"
    //       sh "npm run gh-pages"
    //     }
    //   }
    // }
  }
}