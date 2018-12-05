properties([pipelineTriggers([githubPush()])])
node('linux') {

    stage('Test') {
    
      sh "ant -f test.xml -v";
      junit "reports/result.xml"
      
    }
    
    stage ("Build") {

    ant -f build.xml -v
       
    }
}
