#!groovy

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

properties(
    [
        [
            $class  : 'jenkins.model.BuildDiscarderProperty',
            strategy: [
                    $class      : 'LogRotator',
                    numToKeepStr: '200',
                    daysToKeepStr: '30'
            ]
        ],
        pipelineTriggers(
            [
                [
                    $class: "SCMTrigger", scmpoll_spec: "H/5 * * * *"
                ],
            ]
        ),
        disableConcurrentBuilds()
    ]
)

node('master') {
    try {
	    stage('Version') {
	          dir('verifyJenkins') {

	        // env.VERSION_NAME = "7.5.0"
		    // sh 'pwd'
		    // sh 'll'
		        String readConfigFile = new File("verifyJenkins/gradle/configurations.gradle").text
		        def configLines = readConfigFile.readLines()
		        configLines.each { String line ->
        		    if (line.contains("versionName")) {
            			configVersion = line =~ /(\d+\.)(\d+\.)(\d+)/
            			println "CONFIG VER: = " + configVersion[0][0]
				        env.VERSION_NAME = configVersion[0][0]
        		    }
                    else {
                        env.VERSION_NAME = "7.5.0"
                    }
		        }
	       // }
	    }

        stage('TestVersion') {
            
            dir('verifyJenkins') {
                sh """
                    test=${env.VERSION_NAME}
                    echo \$test
                """
            }
        }

    }  catch (ex) {
        currentBuild.result = "FAILED"
        throw ex
    } finally {
        currentBuild.result
    }
}
