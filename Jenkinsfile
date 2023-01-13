pipeline {
    
	agent any
	
	tools {
        maven "MAVEN3"
        jdk "JAVA_HOME"
    }
    environment{
        SONARSCANNER = 'sonarscanner'
        SONARSERVER = 'sonarserver'
    }

    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

	    stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

        stage('INTEGRATION TEST'){
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }

         stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

        stage('Code Analysis with sonarwube') {
          
		  environment {
             scannerHome = tool "${SONARSCANNER}"
          }

          steps {
            withSonarQubeEnv("${SONARSERVER}") {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
            }

        //     timeout(time: 10, unit: 'MINUTES') {
        //        waitForQualityGate abortPipeline: true
        //     }
           }
        }
        /* 
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
                        docker push aakibvah/vprofiledb:latest
                        docker push aakibvah/vprofileweb:latest
                    '''  
                }
            }
        }*/
    }
}