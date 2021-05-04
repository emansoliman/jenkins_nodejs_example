
pipeline {
    agent any

    stages {
        stage('prepratiom') {
            steps {
                git "https://github.com/emansoliman/jenkins_nodejs_example.git"
        }
         stage('CI') {
            steps {
                   withCredentials([usernamePassword(credentialsId: 'jenkins', passwordVariable: 'mypass', usernameVariable: 'myname')])
                   {
                     sh """
                    docker build . -t emansoliman/myimage:1.0
                    docker login --username $[myname] --password $[mypass]
                    docker push emansoliman/myimage:1.0
                    """
                   }
            }
        }
        
        stage('CD') {
            steps {
                   withCredentials([usernamePassword(credentialsId: 'jenkins', passwordVariable: 'mypass', usernameVariable: 'myname')])
                   {
                   
                   sh """
                    docker run -d -p 3000:3000 emansoliman/myimage:1.0
                    """
                   }
                   
            }
        }
    }
}
