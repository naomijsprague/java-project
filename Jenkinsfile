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
     
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'faad3c54-99a9-46ba-af88-fa6ca34b33b0', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) { 
        
        sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
     
      }
    }
  
}
