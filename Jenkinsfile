@Library('piper-lib-os') _
node() {
    stage('Prepare') { }
    stage('ABAPUnitTests') { gctsExecuteABAPUnitTests script: this}
    stage('Deploy') {
      gctsDeploy script: this
     }
}
