@Library(['piper-lib', 'piper-lib-os']) _
stage('Prepare') {
    node {
      checkout scm
      setupCommonPipelineEnvironment script:this  
    }
}
stage('Test') {
   node {
     dockerExecute(script: this, dockerImage: abaplint/abaplint'){
       echo 'Running abaplint docker'
       sh 'npm install -g @abaplint/cli'
       sh 'abaplint'
       currentBuild.result = 'SUCCESS'                  
     }
   }
} 
stage('Deploy') {
    node {
      gctsDeploy(
          script: this,
          host: 'https://fc-pun01-hana.india.rapidigm.com:8001',
          client: '300',
          abapCredentialsId: 'ABAPUserPasswordCredentialsId',
          repository: 'DEV003',
        )    
    }
} 
stage('Execute ABAP Unit Tests') {
    node { 
        gctsExecuteABAPUnitTests(
            script: this,
            host: 'https://fc-pun01-hana.india.rapidigm.com:8001',
            client: '300',
            abapCredentialsId: 'ABAPUserPasswordCredentialsId',
            repository: 'DEV003',
        )    
    }
}   
stage('Rollback') {
    node { 
        gctsRollback(
            script: this,
            host: 'https://fc-pun01-hana.india.rapidigm.com:8001',
            client: '300',
            abapCredentialsId: 'ABAPUserPasswordCredentialsId',
            repository: 'DEV003',
        )  
    }
}  
                   
