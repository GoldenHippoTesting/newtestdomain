pipeline {
  agent any
  options {
    disableConcurrentBuilds()
  }
  triggers {
      pollSCM('* * * * *')
  }
  stages {
    stage('deploy') {
      when {
        branch 'master'
      }
      steps {
        checkout scm
        sh "aws deploy push --application-name newtestdomain-Application --s3-location s3://newtestdomain-deploy/app.zip --source ./ --region us-west-1"
        sh "aws deploy create-deployment --application-name newtestdomain-Application --s3-location bucket=newtestdomain-deploy,key=app.zip,bundleType=zip --deployment-group-name newtestdomain-CodeDeployGroup-19G11H5VE56UN --description \"Deployed newtestdomain-Application from Jenkins job $JOB_NAME build #$BUILD_NUMBER, by $GIT_COMMITTER_NAME :: $GIT_COMMITTER_EMAIL\" --region us-west-1"
      }
    }
  }
}
