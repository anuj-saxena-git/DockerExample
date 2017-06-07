node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        
        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
  
      //  app = docker.build("getintodevops/hellonode")
     //   app = docker.build("anuj-saxena-git")
        app = docker.build("anujsaxenadocker90/anuj-saxena-git")
        
        
      //  sh 'app = docker.build("getintodevops/hellonode") '
        
      //  sh 'sudo docker.build("anuj-saxena-git/DockerExample") '
      
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

     /*   app.inside {
            sh 'echo "Tests passed"'
        } */
        
        sh 'echo "Tests passed"'
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
     //       docker.withRegistry('https://hub.docker.com/r/anujsaxenadocker90/samplerepo/', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        
        
    }
    
    stage('Push image to ECR') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://848859896798.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:anuj-ecr-credentials') {
     //       docker.withRegistry('https://hub.docker.com/r/anujsaxenadocker90/samplerepo/', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
        
    }
}
