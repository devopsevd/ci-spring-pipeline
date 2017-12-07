node{

    checkout scm
    def mvnHome
    dir('BuildQuality'){
        stage('Preparation'){
                        
            
            git credentialsId: '71d1b4da-7701-4a84-9ecd-48cfb18b5e3b', url: 'https://devopsdemoaws@bitbucket.org/devopsdemoaws/simple-spring-update.git'
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