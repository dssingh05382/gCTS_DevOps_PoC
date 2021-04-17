@Library(['piper-lib', 'piper-lib-os']) _
    stage('prepare') {
        node {
          checkout scm
          setupCommonPipelineEnvironment script:this  
        }
    }
    stage('test') {
       node {
         dockerExecute(script: this, dockerImage: abaplint/abaplint'){
           echo 'Running abaplint docker'
           sh 'npm install -g @abaplint/cli'
           sh 'abaplint'
           currentBuild.result = 'SUCCESS'                  
           }
         }
    }
