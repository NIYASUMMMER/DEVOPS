pipeline {
    agent any
    environment{
        PATH = "/usr/local/bin/:${env.PATH}"
    }
    stages {
        stage ('Virtual environment start') {
            steps {
                echo 'Spinning up the containers'
                //sh '/usr/local/bin/docker-compose build'
                //sh '/usr/local/bin/docker-compose up'
                sh '/usr/local/bin/docker-compose up --build'
            }      
        }
//         stage('Manage Dependancies') {
//             steps {
//                 sh 'npm install'
//                 echo 'Managing dependancies'
//             }
//         }
    
        stage('MicroServices - Startup in Parallel') {


            parallel {


                stage('Authentication') {
                    steps {
                        dir('Authetication'){
                        echo 'Authentication starting up'
                        sh 'npm install' 
                        }
                    }
                }
        }
    }
}

//                 stage ('Patients MicroService') {
//                     steps {
//                         dir('PatientRegistration'){
//                         echo 'Patients Service starting up'
//                         bat 'npm install'
//                         }
//                     }
//                 }
//                 stage ('Ward Admissions starting up') {
//                     steps {
//                         dir('WardManager'){
//                         echo 'Staff MicroService starting up'
//                         bat 'npm install'
//                         }
//                     }
//                 }
//             }      
//         }
                stage('Unit Testing - Chai/Mocha') {
            steps {   
                   dir('PatientRegistration') {
                                script {
                                echo 'Patient database Testing with Chai/Mocha'
                                 bat 'npm test'
                                    }
                                }
                    }
        }             

//         stage('Microservice containers build') {
//                 steps {
//                      dir('PatientRegistration') {
//                     script {
//                     echo 'Spinning down running containers'
                    
//                     sh 'docker-compose down'
                
//                     echo 'Spinning up the containers'
//                     sh 'docker-compose build'
//                     }
//                     }
//                 }}


//         stage('deploy') {
//             steps {
//                  dir('PatientRegistration') {
//                 script {
//                 bat 'docker-compose up -d'
//                 echo 'MicroServices are being deployed in Dockers'
//                     }
//                 }
//             }}
//     }
        post {
            always {
                echo 'Pipeline fully executed.'
            }
            success {
                echo 'All stages completed successfully.'
            }
            unstable {
                echo 'Stages are inconsistent'
            }
            failure {
                echo 'Pipeline Failed'
            }
            changed {
                echo 'Changes detected..'
            }
        }
}
            
