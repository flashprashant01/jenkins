node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("prashant01/jenkins")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
     withCredentials([usernamePassword(credentialsId: 'dockerhub1', passwordVariable: 'dockerhub1Password', usernameVariable: 'dockerhub1User')]){
          sh "docker login -u ${env.dockerhub1User} -p ${env.dockerhub1Password}"
         app.push("${env.BUILD_NUMBER}")
        }         
    }
   // stage('Run deployment'){
     //  sh 'kubectl run nginx --image=anand91073/dell --port=80'
    }
   // stage('Expose service'){
     //   sh 'kubectl expose deployment nginx --type=NodePort'    
 //   }
// }
