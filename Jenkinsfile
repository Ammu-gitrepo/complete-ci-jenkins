pipeline{
    agent any
    tools{
        maven 'MAVEN3'
        jdk 'OracleJDK8'
    }

    environment {
        SNAP_REPO = 'vprofile-release-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'Ammu@1996'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vprofile-dependency-release'
		NEXUSIP = '172.31.22.141'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vprofile-group-repo'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test'){
            steps{
                sh 'mvn -s settings.xml test'
            }
        }
        stage('Code Analysis'){
            steps{
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
    }

}