node("BuildServer"){

    checkout scm
    def mvnHome
    dir('BuildQuality'){
        stage('Preparation'){
                        
            
            git credentialsId: '9957a419-6d9b-4139-b297-3ed9658faa03', url: 'https://devopsdemoaws@bitbucket.org/devopsdemoaws/simple-spring-update.git'
            mvnHome = tool 'Maven'
        }

        stage('Build') {
            // Run the maven build
            if (isUnix()) {
                sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
            } else {
                bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
            }
        }
    }
}