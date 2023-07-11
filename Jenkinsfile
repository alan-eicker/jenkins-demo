pipeline {

  agent any

  tools {nodejs "Node.js 18.15.0"}
  
  parameters {
    booleanParam(defaultValue: true, description: "Enable Service?", name: "myBoolean")
    choice(choices: ["TEST","DEV","QA","PREPROD","PROD"], description: "Which environment to deploy to?", name: "deployEnv")
  }

  environment {
    def myEnv = "devlopment"
    def myNum = 10
  }

  stages {
    stage("Build Info") {
      steps {
        echo "********** Checking Params **********"
        echo "BooleanParam set to: ${params.myBoolean}"
        echo "Deploying to: ${params.deployEnv}"
        echo "Environment var: ${myEnv}";
        echo "Build Number: ${env.BUILD_NUMBER}";

        myFunc("blah, blah!!", 20);

        script {
          if (params.deployEnv == "PROD") {
            echo "RUNNING IN 'PROD' MODE."
          }
        }
      }
    }
    stage("Cleanup") {
      steps {
        deleteDir()
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
    stage("Build Remote"){
      steps {
        echo "********** Building remote **********"
        build job: "Jenkins-Demo", parameters: [[{$class: "booleanParamValue", name: "myBoolean", value: false }]]
      }
    }
  }
}

def myFunc(String myText, int myNumber) {
  echo "myNumber set to: ${myNumber}"
  echo "myText set to: ${myText}"
}