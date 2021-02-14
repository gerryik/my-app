    node('maven-label') {
        def mvnHome
        stage('Preparation'){
            git 'https://github.com/gerryik/my-app.git'
            mvnHome= tool 'maven3'
        }
        stage('Build') {
            
            withEnv(["MVN_HOME=$mvnHome"]){
                if(isUnix()){
                sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore=true clean package'
                }
                else { 
                    bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore=true clean package/)
                }
            }
        }
        stage('Results') {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                
            }
        }
    }
