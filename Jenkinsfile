pipeline{
    agent any
    stages{
        stage("Code of Git"){
            steps{
                git url: "https://github.com/ujer23/two-tier-flask-app.git" , branch: "master"
            }
            }
            stage("Build"){
            steps{
                sh "docker build -t demo-jen:latest ."
            }
            }
                stage("Test"){
            steps{
                echo "code is testing"
            }
                }
                stage("Docker hub "){
                    steps{
                        withCredentials([usernamePassword(
                            credentialsId:"docker-jenkins",
                            usernameVariable: "uju",
                            passwordVariable: "uji"
                        )]){
                        sh """ 
                        echo $uji | docker login -u $uju --password-stdin
                        docker tag demo-jen:latest $uju/jenkins-to-docker:latest
                        docker push $uju/jenkins-to-docker:latest
                        """
                        }
                    }
                }
                stage("Deploy"){
                    steps{
                        sh "docker compose up -d --build"
                    }
                    
                }
    }
}
