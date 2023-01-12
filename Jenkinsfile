pipeline {
    
	agent any
	
	tools {
        maven "MAVEN3"
        jdk "JAVA_HOME"
    }
 
    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
            // post {
            //     success {
            //         echo 'Now Archiving...'
            //         archiveArtifacts artifacts: '**/target/*.war'
            //     }
            //}
        }

	    stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

        stage('Building images'){
            steps {
                sh '''
                    docker build -f Docker-files/app/Dockerfile -t aakibvah/vprofileapp .
                    docker build -f Docker-files/db/Dockerfile -t aakibvah/vprofiledb .
                    docker build -f Docker-files/web/Dockerfile -t aakibvah/vprofileweb .
                '''
            }
        }

        stage('Pushing images'){
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerlogin', passwordVariable: 'Password', usernameVariable: 'User_Name')]) {
                    sh '''
                        docker login -u ${User_Name} -p ${Password}
                        docker push aakibvah/vprofileapp:latest
                        docker push aakibvah/vprofileadb:latest
                        docker push aakibvah/vprofileweb:latest
                    '''  
                }
            }
        }
    }
}