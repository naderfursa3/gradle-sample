pipeline {
    
    agent any
    
    stages{
        
        stage('Setup Parameters') {
            steps {
                script {
                    properties(
                        [parameters([
                            choice(choices: ['jar', 'tar', 'zip'], 
                            description: 'Please Choose the Artifact Type To Create',
                            name: 'ARTIFACT_TYPE')
                            ]) 
                        ])
                }                
            }
        }
        //
        stage('Clone from Github') {
            steps {
                git branch: 'main', url:'https://github.com/naderfursa3/gradle-sample.git'
            }
        }
        //
        stage('Build JAR') {
            when {
                expression {
                    return params.ARTIFACT_TYPE == "jar"
                }
            }
            steps{
                script{
                    dir('complete') {
                        sh "./gradlew clean jar"
                }
            }
        }
     }
    //
    stage('Build TAR') {
        when {
            expression {
                return params.ARTIFACT_TYPE == "tar"
            }
        }
        steps{
            script{
                dir('complete') {
                    sh "./gradlew clean distTar"
                }
            }
        }
    }

    stage('Build ZIP') {
        when {
            expression {
                return params.ARTIFACT_TYPE == "zip"
            }
        }
        steps{
            script{
                dir('complete') {
                    sh "./gradlew clean distZip"
                }
            }
        }
    }


}
}