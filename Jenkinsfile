#!groovy

node {
  def sbtHome = tool 'default-sbt'
  //def SBT = "${sbtHome}/bin/sbt -Dsbt.log.noformat=true -Dsbt.override.build.repos=true"
  def SBT = "${sbtHome}/bin/sbt -Dsbt.log.noformat=true"

  def branch = env.BRANCH_NAME

  echo "current branch is ${branch}"

  // Mandatory, to maintain branch integrity
  checkout scm

  stage('Cleanup') {
    sh "${SBT} clean"
  }

  stage('Build') {
    sh "${SBT} package"
  }

  stage('Publish-Local') {
    sh "${SBT} publish-local"
  }

  stage('Archive') {
    archive 'target/**/test-dep*.jar'
  }

}
