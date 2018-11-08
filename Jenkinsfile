#!groovy
node ('master'){

	try {
	    stage('Preparation') {
			git branch: 'master', url: 'https://github.com/saiteja1141/https-saiteja1141-gmail.com-scm-tma-genesis-android.git'

			}
		stage('Version') {

	          dir('https-saiteja1141-gmail.com-scm-tma-genesis-android') {

	           //env.VERSION_NAME = "7.5.0"
		       sh 'pwd'
		      // sh 'ls'
		        File readConfigFile = new File('/var/jenkins_home/workspace/updateVersion/https-saiteja1141-gmail.com-scm-tma-genesis-android/verifyJenkins/gradle/configurations.gradle')
			def configLines = readConfigFile.readLines()
			configLines.each { 
				String line ->
					if (line.contains("versionName")) {
					def configVersion = line =~ /(\d+\.)(\d+\.)(\d+)/
					print "CONFIG VER: = " + configVersion[0][0]
					env.VERSION_NAME = configVersion[0][0]
					}
				
				}
			}
		}

		stage('jenkinsnew') {
            
            dir('jenkinsTest') {
                sh """
                    test=${env.VERSION_NAME}
                    echo \$test
                """
            }
        }

    }
  catch (ex) {
        currentBuild.result = "FAILED"
        throw ex
    }
} 