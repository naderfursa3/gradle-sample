pipeline {
    
    agent any
    //
    parameters {
        choice (
            name: 'ARTIFACT_TYPE',
            choices: ['jar', 'tar', 'zip'],
            description: 'Please Choose the Artifact Type To Create'
        )
    }
    //
    stages{
        
        environment{
            MY_VAR='NADER'
        }
        
        // stage('Setup Parameters') {
        //     steps {
        //         script {
        //             properties(
        //                 [parameters([
        //                     choice(choices: ['jar', 'tar', 'zip'], 
        //                     description: 'Please Choose the Artifact Type To Create',
        //                     name: 'ARTIFACT_TYPE')
        //                     ]) 
        //                 ])
        //         }                
        //     }
        // }
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
                    echo env.MY_VAR
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