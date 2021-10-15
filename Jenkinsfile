node('slave1') { 
 gradle4 = tool 'gradle4'
 currentBuild.result = "SUCCESS"
 try {
  stage ('checkout'){
     checkout scm
  }
  stage ('build')
  {
      sh "${gradle4}/bin/gradle build"
  }
  stage ('test')
  {
      sh "${gradle4}/bin/gradle" test"
  }
 } catch (ex) {
  currentBuild.result = "FAILURE"
  echo 'Error occured'
 }
 stage ('tests') {
  tests = ["one" : { sh "test-data/int-test.shbuild/libs/oto-gradle-1.0.jar otoMato 'Hello Otomato!'"},
           "two" :{ sh "test-data/int-test.shbuild/libs/oto-gradle-1.0.jar otoMato 'Hello Sashok!'" },
           "three" :{ sh "test-data/int-test.shbuild/libs/oto-gradle-1.0.jar otoMato 'Hello Anton!'" }
           }
 stage('post') {
  echo "Build result is " + currentBuild.result
  if ( currentBuild.result == 'SUCCESS') {
   addBadge(icon: 'green.gif', text: 'Build Succeeded')
   archiveArtifacts artifacts: 'generatedFile.txt', onlyIfSuccessful: true
  }
  if (currentBuild.result == 'FAILURE') {
   addBadge(icon: 'red.gif', text: 'Build Failed')
  } 
 }
}
