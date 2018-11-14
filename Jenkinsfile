#!groovy
node ('master'){

	try {
	    stage('Preparation') {
			git branch: 'master', url: 'https://github.com/saiteja1141/https-saiteja1141-gmail.com-scm-tma-genesis-android.git'

			}
		stage('Version') {

	          dir('verifyJenkins') {
		
		def configurationGradle = readFile("./gradle/configurations.gradle")
                def configVersion = configurationGradle =~ /(versionName\s+:\s+\")(\d+\.)(\d+\.)(\d+)/
                print "configurations.gradle:" configVersion
                print configVersion.split(':')[1]
                env.VERSION_NAME = configVersion.split(':')[0]      
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