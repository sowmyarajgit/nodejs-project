def registry = 'https://sowmyaraj15.jfrog.io'
def imageName = 'sowmyaraj15.jfrog.io/nodejs-docker-local/nodejs-project'
def version   = '1.0.2'
pipeline{
    agent {
        node {
            label "ansible"
        }
    }

    //tools {nodejs 'nodejs-16'}

    //stages {
      //  stage('gitclone') {
        //    steps {
          //    git branch: 'main', url: 'https://github.com/sowmyarajgit/nodejs-project.git'  
            //}
        //}

    stages {
         
         stage('gitclone') {
            steps {
              git branch: 'main', url: 'https://github.com/sowmyarajgit/nodejs-project.git'  
            }
        }


        stage('build') {
            steps{
                echo "------------ build started ---------"
               	sh "npm install"
                echo "------------ build completed ---------"
        }
      }

        stage('Unit Test') {
            steps {
                echo '<--------------- Unit Testing started  --------------->'
                sh 'npm test'
                echo '<------------- Unit Testing stopped  --------------->'
            }
        }

stage(" Docker Build ") {
      steps {
        script {
           echo '<--------------- Docker Build Started --------------->'
           app = docker.build(imageName+":"+version)
           echo '<--------------- Docker Build Ends --------------->'
        }
      }
    }

    stage (" Docker Publish "){
        steps {
            script {
               echo '<--------------- Docker Publish Started --------------->'  
                docker.withRegistry(registry, 'jfrog1111'){
                    app.push()
                }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
        }
    }
    //         stage('Deployment') {
    //         steps {
    //             echo '<--------------- deployment started  --------------->'
    //             sh './deploy.sh'
    //             echo '<------------- deployment stopped  --------------->'
    //         }
    //     }  
     }
     }
