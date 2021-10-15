node('slave1') { 
 gradle4 = tool 'gradle4'
 currentBuild.result = "SUCCESS"
 try {
  stage ('checkout'){
     checkout scm
  }
  stage ('build')
  {
      sh "${gradle4}/bin/gradle clean build"
  }
  stage ('test')
  {
      sh "${gradle4}/bin/gradle test"
      junit 'build/test-results/junit-platform/*.xml'
  }
 } catch (ex) {
  currentBuild.result = "FAILURE"
  echo 'Error occured'
 }
 stage ('tests') {
  tests = ["one" : { sh "sh test-data/int-test.sh build/libs/oto-gradle-1.0.jar otoMato 'Hello Otomato!'"},
           "two" : { sh "sh test-data/int-test.sh build/libs/oto-gradle-1.0.jar otOmAto 'Hello Sashok!'"},
           "three" : { sh "sh test-data/int-test.sh build/libs/oto-gradle-1.0.jar OToMatO 'Hello Anton!'"}]
           parallel tests
           }
 stage('post') {
  echo "Build result is " + currentBuild.result
  if ( currentBuild.result == 'SUCCESS') {
   addBadge(icon: 'green.gif', text: 'Build Succeeded')
   //archiveArtifacts artifacts: 'gradle.txt', onlyIfSuccessful: true
  }
  if (currentBuild.result == 'FAILURE') {
   addBadge(icon: 'red.gif', text: 'Build Failed')
  } 
 }
}
