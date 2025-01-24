pipeline {
  //  agent any
  options {                                                          #Options defines the behaviour of the job
      disableConcurrentBuilds()                                      #concurrentbuild=at a time many people click on builds                                
  timeout(time: 1, unit: 'HOURS')                                #it is the time that if the job not yet completed within that time then it gets kills  itself                                                                                                                                               disableResume()                                               #resume diable means if 1 stage gets stop, next stage shd not get start 
    }
    triggers {
        cron('H */4 * * 1-5')
    }
    parameters {                                                      #to take the inputs
        string(name: 'STRING_VARIABLE', defaultValue: 'TestTrainer', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    environment {                                    #doubt
        def name = "my name"
        def pwdv = ""
    }
  stages {
    stage('Clean Workspace') {
      steps {
        cleanWs()
      }
    }
    stage('Loop') {
      steps {
        echo 'Hello World'

        script {
          def browsers = ['chrome', 'firefox']
          for (int i = 0; i < browsers.size(); ++i) {
            echo "Testing the ${browsers[i]} browser"
          }
        }
      }
    }
    stage('Validate') {
      // when { branch 'master' }	
      steps {
        script {
          if ("${STRING_VARIABLE}" == "TestTrainer") {
            error 'Triggered error'
          } else {
            echo "The input was different from TestTrainer so proceeding"
          }
        }
      }
    }
    stage('Confirm button') {
      steps {
        input 'Please confirm'
        sh("echo asdasdasd")
      }
    }
    stage('Child Jobs') {
      steps {
        build quietPeriod: 6, wait: true, job: 'VJ_Pipeline'
        build quietPeriod: 6, wait: true, job: 'VJ_Pipeline'
        build quietPeriod: 6, wait: true, job: 'VJ_Pipeline'
        build quietPeriod: 6, wait: true, job: 'VJ_Pipeline'
        build quietPeriod: 6, wait: true, job: 'VJ_Pipeline'
      }
    }

    stage('Parallel Stage') {
      // when { branch 'master' }
      failFast true
      parallel {
        stage('Branch A') {
          /* agent {
              label "master"
            }*/
          steps {
            echo "On Branch A"
          }
        }
        stage('Branch B') {
          /*agent {
            label "master"
          }*/
          steps {
            echo "On Branch B"
          }
        }
      }
    }
    stage('GIt Clone Branch') {
      steps {
        git branch: 'main', url: 'https://github.com/Arvind9719/hello-world.git'
        dir('MOVE') {
          sh("touch test.txt")
          sh("cat test")
          readFile 'test'
        }
      }
    }
    stage('Trainer') {
      steps {
        script {
          sh("echo ${STRING_VARIABLE}")
        }
      }
    }
    stage('Variable Initialization') {
      steps {
        script {
          sh("echo ${name}")
          writeFile file: 'test-write-file', text: 'asdasdasdasdasd'
        }
      }
    }

  }
}
