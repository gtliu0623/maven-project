pipeline {
    
    agent any
    tools {
        maven 'local maven'
    }
    
 	stage('Build') {
            steps {
                echo "Building....."
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "開始存檔"
                    arlchiveArtifacs artifacts '**/target/*.war'
                }
            }

    }

}