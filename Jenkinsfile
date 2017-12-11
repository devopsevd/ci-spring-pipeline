node("BuildServer"){
    checkout scm
    def mvnHome
    dir('BuildQuality'){
        stage('Preparation'){                      
            git url: 'https://github.com/devopsevd/ci-spring.git'
            mvnHome = tool 'Maven'
        }

        stage('Build') {
                sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
        }
    }
}

node("BuildServer") {
        stage("Deploy to test") {
        dir('BuildQuality'){
        sh 'sudo docker-compose up -d --build'
        }                
    }
}

node("BuildServer") {
    def mvnHome
    dir('FunctionalTests'){
            stage('Get Functional Test Scripts'){                        
                git 'https://github.com/devopsevd/ci-sping-selenium.git'
                mvnHome = tool 'Maven'
            }
            stage('Run Tests') {
                sh "'${mvnHome}/bin/mvn' -Dgrid.server.url=http://10.144.2.237:4444/wd/hub clean test "
            }
            stage('Functional Test Results') {
            junit '**/target/surefire-reports/TEST-*.xml'
            }
    }
}

node("BuildServer") {
    dir('BuildQuality'){
            stage("Shutdown staging"){          
                sh 'sudo docker-compose stop'
            }
    }    
}
