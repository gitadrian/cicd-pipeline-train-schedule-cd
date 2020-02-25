pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Deploy to Stage'){
            when{
             branch 'master'
            }
            steps{
               withCredentials([usernamePaswword(credentialsId:'webserver_login', usernameVariable: 'USERNAME', passwordVariable:'USERPASS')]){
               
                sshPublisher(
                   failOnError: true,
                   continueOnError: false,
                    publishers:[
                     configName:'staging',
                     sshCredentials:[
                      username:"$USERNAME",
                       encryptedPassphrase:"$USERPASS"
                     ]
                    ]
                    
                )
               
               }
            }
        }
    }
}
