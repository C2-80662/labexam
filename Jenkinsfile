pipeline {
    agent any

    stages {
        stage ('fetch repository') {
            steps {
                git branch: 'master', url:  'https://github.com/C2-80662/labexam.git'
            }
        }
        stage ('docker build a new image') {
            steps {
                sh '/usr/bin/docker image build -t punammakh/myimage .'
            }
        }
        stage ('docker non-interactive login'){
         steps {
                sh 'echo dckr_pat_CV4X-q8OWzs3fpn_aCl9hnxEYbw | /usr/bin/docker login -u punammakh --password-stdin'
            }
        }

        stage ('docker push image') {
            steps {
                sh '/usr/bin/docker image push punammakh/myimage'
            }
        }
        stage ('docker remove service') {
            steps {
                sh '/usr/bin/docker service rm myservice'
            }
        }
        stage ('docker create service') {
            steps {
                sh '/usr/bin/docker service create --name myservice --replicas 5 -p 9876:80 punammakh/myimage'
            }
        }
    }
}
