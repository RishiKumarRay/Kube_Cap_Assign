pipeline{
    agent any
   /* environment {
        dockerhub=credentials('dockerhub')
        
    } */
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

       
      /*  stage('build image')
        {
            when{
                branch "prod"
                }
            steps{
                sh 'docker build -t capstone-img:1.01 .'
            }
        } 

        stage('pushing to dockerhub')
        {
            when{
                branch "prod"
                }
            steps{
                sh 'docker tag capstone-img:1.01 rishivantsingh9717/capstone:1.01 '
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'

                sh 'docker push rishivantsingh9717/capstone:1.01 '
            }
        } */

    }
}
