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
                sh 'docker build -t myimage:1.01 .'
            }
        } 

        stage('pushing to dockerhub')
        {
            when{
                branch "Production"
                }
            steps{
                sh 'docker tag myimage:1.01 rishiray/springboot:1.01'
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'

                sh 'docker push rishiray/springboot:1.01'
            }
        } 

    }
}
