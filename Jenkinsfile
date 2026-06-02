pipeline{
    agent any
    stages{
        stage('build app'){
            steps{
                sh 'mvn clean package -DskipTests'
                echo 'build successful'
            }
        }

        stage('test app'){
            steps{
                sh 'mvn test'
                echo 'test successful'
            }
        }

        stage('build image'){
            steps{
                sh 'docker build -t adhammamdouh272/java-app'
                echo 'Docker image built successfully successful'
            }
        }
        
        stage('push'){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                    sh 'docker login --username $Username --password $Password'
                    sh 'docker tag java-app $Username/java-app'
                    sh 'docker push $Username/java-app'
                    }
                }
            }
        }     
    }
}
