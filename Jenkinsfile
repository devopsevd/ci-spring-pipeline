node("BuildServer"){

    checkout scm
    def mvnHome
    dir('BuildQuality'){
        stage('Preparation'){
                        
            
            git url: 'https://github.com/devopsevd/ci-spring.git'
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
