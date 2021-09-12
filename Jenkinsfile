pipeline {
    agent any
    tools {
        maven 'local maven'
    }
    
    stages {
        stage('Build') {
            steps {
                echo "Building....."
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "開始存檔"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }   

        stage('Deploy to staging') {
            steps {
                build job: 'maven project deploy-to-staging'
            }
        }

        stage('Deploy to production') {
            steps {
                timeout(time: 5, unit: 'DAYS') {
                    input message: '是否佈署到生產環境'
                }

                build job: 'maven project deploy-to-production'
            }
            post {
                success {
                    echo '代碼成功佈署到生產環境'
                }

                failure {
                    echo '佈署失敗'
                }
            }
        }

    }
 	
}
