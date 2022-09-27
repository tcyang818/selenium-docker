// pipeline {
//     agent none
//     stages {
//         stage('Build Jar') {
//             agent {
//                 docker {
//                     image 'maven:3-alpine'
//                     args '-v $HOME/.m2:/root/.m2'
//                 }
//             }
//             steps {
//                 sh 'mvn clean package -DskipTests'
//             }
//         }
//         stage('Build Image') {
//             steps {
//                 script {
//                 	app = docker.build("tcyang818/selenium-docker")
//                 }
//             }
//         }
//         stage('Push Image') {
//             steps {
//                 script {
// 			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
// 			        	app.push("${BUILD_NUMBER}")
// 			            app.push("latest")
// 			        }
//                 }
//             }
//         }
//     }
// }
pipeline {
    // master executor should be set to 0
    agent any
    stages {
        stage('Build Jar') {
            steps {
                //sh, bat
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Build Image') {
            steps {
                //sh, bat
                sh "docker build -t='tcyang818/selenium-docker' ."
            }
        }
        stage('Push Image') {
            steps {
			    withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'yang123@@@', usernameVariable: 'tcyang818')]) {
                    //sh, bat
			        sh "docker login --username='tcyang818' --password='yang123@@@'"
			        sh "docker push tcyang818/selenium-docker:latest"
			    }
            }
        }
    }
}