pipeline{
    agent any
    environment {
        dockerhub=credentials('dockerhub')
        
    } 
    stages{
        stage('clean')
        {
            steps{
                sh 'mvn clean'
            }
        }

        stage('test')
        {
            steps{
                sh 'mvn test'
            }
        }

        stage('pack')
        {
            when{
                branch "Production"
                }
            steps{
                sh 'mvn package'
            }
        }

       
        stage('build image')
        {
            when{
                branch "Production"
                }
            steps{
                sh 'docker build -t myimage:${GIT_COMMIT} .'
            }
        } 

        stage('pushing to dockerhub')
        {
            when{
                branch "Production"
                }
            steps{
                sh 'docker tag myimage:${GIT_COMMIT} rishiray/springboot:${GIT_COMMIT}'
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'

                sh 'docker push rishiray/springboot:${GIT_COMMIT}'
            }
        } 

    }
}
