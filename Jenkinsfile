pipeline {
  agent any
  options {
    buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3')
  }    
  environment {
    TOMCAT_CREDS=credentials('tomCreds20') // Refers to the SSH key added in Jenkins
    TOMCAT_SERVER="10.0.0.20"
    ROOT_WAR_LOCATION="/opt/tomcat/webapps"
    LOCAL_WAR_DIR="build/dist"
    WAR_FILE="app-0.1.0.war"
  }
  stages {
    // stage('verify tooling') {
    //   steps {
    //     sh '''
    //       chmod +x ./bld
    //       java -version
    //       ./bld version
    //     '''
    //   }
    // }
    // stage('download') {
    //   steps {
    //     sh './bld download purge'
    //   }
    // }
    // stage('compile') {
    //   steps {
    //     sh './bld clean compile'
    //   }
    // }
    // stage('precompile') {
    //   steps {
    //     sh './bld precompile'
    //   }
    // }
    // stage('test') {
    //   steps {
    //     sh './bld test'
    //   }
    // }
    // stage('war') {
    //   steps {
    //     sh './bld war'
    //   }
    // }  
    stage('copy the war file to the Tomcat server') {
      steps {
        scripts {
          sshagent(['tomCreds20']) {
            sh '''
            ssh -o StrictHostKeyChecking=no $TOMCAT_CREDS_USR@$TOMCAT_SERVER "echo login_successfull"
            '''
          }
        }
      }
    }
  }
}// ssh -i $TOMCAT_CREDS $TOMCAT_CREDS_USR@$TOMCAT_SERVER "rm -rf $ROOT_WAR_LOCATION/ROOT; rm -f $ROOT_WAR_LOCATION/ROOT.war"
          // scp -i $TOMCAT_CREDS $LOCAL_WAR_DIR/$WAR_FILE $TOMCAT_CREDS_USR@$TOMCAT_SERVER:$ROOT_WAR_LOCATION/ROOT.war
          // ssh -i $TOMCAT_CREDS $TOMCAT_CREDS_USR@$TOMCAT_SERVER "chown $TOMCAT_CREDS_USR:$TOMCAT_CREDS_USR $ROOT_WAR_LOCATION/ROOT.war"
          // ssh -i $TOMCAT_CREDS $TOMCAT_CREDS_USR@$TOMCAT_SERVER "/opt/tomcat/bin/catalina.sh start"