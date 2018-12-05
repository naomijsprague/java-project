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

    sh "aws s3 cp /workspace/java-pipeline/dist/rectangle-*.jar seis665-03-nspra1328" 
   }
}
