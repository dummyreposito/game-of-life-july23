pipeline {
    agent {label ' JDK_8'}
    options{
        retry(3)
        timeout(time: 1, unit: 'MINUTES')
    }
        triggers{
            pollSCM('* * * * *')
        }
        tools {
            jdk 'JAVA_8'
        }
        stages{
            stage('VCS'){
                steps{
                    git url: 'https://github.com/dummyreposito/game-of-life-july23.git',
                        branch: 'master'
                }
            }
            stage('build and package'){
                steps{
                    sh script: 'mvn clean package'
                }
            }
            stage('archieve and publish junittest results'){
                steps{
                    archiveArtifacts artifacts: '**/target/gameoflife.war'
                    junit testResults: '**/surefire-reports/TEST-*.xml' 
                }
              
            }
           
        }

        post {
            success {
                mail subject: 'your build is success',
                     body: 'Hi this jenkins job',
                     cc: 'ajaykumar.matters@gmail', 
                     from: 'info@test.com',
                     to: 'admin@jenkins.com'
            }
            
            failure {
                mail subject: 'your build is failed',
                     body: 'Hi this jenkins job',
                     cc: 'ajaykumar.matters@gmail', 
                     from: 'info@test.com',
                     to: 'admin@jenkins.com' 
            }
        }
}

