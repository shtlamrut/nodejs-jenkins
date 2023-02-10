node {
     def app 
     stage('Initialize'){
        def dockerHome = tool 'docker'
        def nodeHome = tool 'node'
          env.PATH = "${dockerHome}/bin:${nodeHome}/bin:${env.PATH}"
    }
     stage('clone repository') {
      checkout scm  
    }
     stage('Build docker Image'){
      app = docker.build("shtlamrut/dockerdemo")
    }
     stage('Test Image'){
       app.inside {
         sh 'echo "TEST PASSED"'
      }  
    }
     stage('Push Image'){
       docker.withRegistry('https://registry.hub.docker.com', 'git') {            
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")   
   }
}
}
