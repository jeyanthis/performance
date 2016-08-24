#!groovy
node ('master') {
   stage 'Checkout Performance Repo'

   // Get some code from a GitHub repository
   checkout scm

   def version = release_version()
   
   stage "Setting Release Version to ${version}"
   mvn "versions:set -DnewVersion=${version}"
   
   stage 'Build Docker Images'
   mvn "docker:build"
   
   stage 'Push Docker Images'
   mvn "docker:push"
   
   stage 'Prep for next Iteration'
   mvn "release:update-versions -DautoVersionSubmodules=true"
   
   stage 'Publish'
   mvn "scm:checkin -Dmessage=\"[jenkins-pipeline] Prepare for next development iteration\""
}


def mvn(args) {
  sh "mvn ${args}"
}

def release_version() {
  def pom = readMavenPom file: 'pom.xml'
  pom.version.replace("-SNAPSHOT". "")
}
