pipeline{
    agent any
    environment { 
        registry = "kunalgarg8077/kunal_capstone" 
        registryCredential = 'kunal' 
        dockerImage = '' 
    }    
    tools { 
        maven 'maven3'
    }
    stages
       {
          stage("Build")
            {
                steps{
                    sh "mvn compile"
                }
                
            }
            stage("Test")
            {
                steps{
                    sh "mvn clean test"
                }
            }
            stage("Package")
            {
                steps{
                    sh "mvn clean package"
                }
            }
            stage('Building our image') { 
                steps { 
                    script { 
                        dockerImage = docker.build registry + ":$GIT_COMMIT-$BUILD_NUMBER"
                    }
                } 
            }
            stage('save our image') { 
                steps { 
                    script { 
                        docker.withRegistry( '', registryCredential ) { 
                            dockerImage.push() 
                        }
                    } 
                }
            }

      }
}
