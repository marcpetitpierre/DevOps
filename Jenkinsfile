pipeline {
    agent { label 'jenkinslave' }
    stages {
        stage('Fetch dependencies') {
        /* This stage pulls the latest nginx image from
           Dockerhub */
            steps {
                sh 'sudo docker pull nginx:latest'
          }
        }
        stage('Build docker image') {
        /* This stage builds the actual image; synonymous to
           docker build on the command line */
            steps {
            sh "sudo docker build . -t customnginx:1"
            }    
        }
        stage('Test image') {
         /* This stage runs unit tests on the image; we are
            just running dummy tests here */
            steps {
                sh 'echo "Tests successful"'
          }
        }
        stage('Push image to OCIR') {
         /* Final stage of build; Push the 
            docker image to our OCI private Registry*/
        steps {
            sh "sudo docker login -u 'oci_core_emea_acs_petitpierre/account.manager@oracle.com' -p 'pIol0BX:-B{7TJl8rrD)' zrh.ocir.io"
            sh "sudo docker tag customnginx:1 zrh.ocir.io/oci_core_emea_acs_petitpierre/nginx:custom"
            sh 'sudo docker push zrh.ocir.io/oci_core_emea_acs_petitpierre/nginx:custom'
            
           }
         }      
    }
}
