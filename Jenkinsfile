#!groovy
node ('master'){

	try {
	    stage('Preparation') {
			git branch: 'master', url: 'https://github.com/saiteja1141/https-saiteja1141-gmail.com-scm-tma-genesis-android.git'

			}
		stage('Version') {

	          dir('verifyJenkins') {
		
def configurationGradle = readFile("./gradle/configurations.gradle")
                print "configurations.gradle: ${configurationGradle}"
                File file = File.createTempFile("temp", ".temp")
                file.write configurationGradle
                def configLines = file.readLines()
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