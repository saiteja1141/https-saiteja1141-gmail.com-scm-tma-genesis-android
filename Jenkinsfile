#!groovy
node ('master'){

	try {
	    stage('Preparation') {
			git branch: 'master', url: 'https://github.com/saiteja1141/https-saiteja1141-gmail.com-scm-tma-genesis-android.git'

			}
		stage('Version') {

			dir('verifyJenkins') {
		
				def configurationGradle = readFile("./gradle/configurations.gradle")
				println configurationGradle
                		def configVersion = configurationGradle =~ /(versionName\s+:\s+\")(\d+\.)(\d+\.)(\d+)/
				print "VersionName:" + configVersion[0][0].split('"')[1]
				print “Setting VERSION_NAME to ${env.VERSION_NAME}” 
                		env.VERSION_NAME = configVersion[0][0].split('"')[1]
				//println “Setting VERSION_NAME to ${env.VERSION_NAME}” 
				//print "Setting ${VERSION_NAME} to ${env.VERSION_NAME}"     	
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