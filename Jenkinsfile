 pipeline{
            tools{
                jdk 'myjava'
                maven 'mymaven'
            }
            agent none
            stages{
                stage('Checkout on Master'){
                    agent any
                    steps{
                echo 'cloning...'
                        git 'https://github.com/elormalade/DevOpsClassCode.git'
                    }
                }
                stage('Compile on Slave11'){
                    agent {label 'Slave11'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview on Slave11'){
                    agent {label 'Slave11'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest on Slave22'){
                    agent {label 'Slave22'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package on Master'){
                    agent any
                    steps{
                        sh 'mvn package'
                    }
                }
            }
        }
