properties([pipelineTriggers([githubPush()])])
node('linux') {

    stage("Unit Tests") {
      git 'https://github.com/naomijsprague/java-project.git'
      sh "ant -f test.xml -v";
      junit "reports/result.xml"
      
    }
    
    stage ("Build") {

      sh "ant -f build.xml -v"
       
    }

    stage ("Deploy"){

      sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar s3://seis665-03-nspra1328" 
   
    }

    stage ("Report"){
     
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
 
        sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
     
      }
    }
  
}
