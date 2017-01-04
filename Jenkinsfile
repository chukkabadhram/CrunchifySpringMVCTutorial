#!groovy
node {
      def mvnHome
   checkout scm
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/chukkabadhram/CrunchifySpringMVCTutorial'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
            // let's run the wondows
         bat(/"${mvnHome}\bin\mvn" clean package/)
      }
   }
   stage('UnDeploy') {
      bat(/"${mvnHome}\bin\mvn" tomcat7:undeploy/)
   }
   stage('Deploy') {
      bat(/"${mvnHome}\bin\mvn" tomcat7:deploy/)
   }
}
