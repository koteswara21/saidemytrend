def registry = 'https://kotidemy.jfrog.io/'

pipeline {                                    

    agent any                                 

    environment {                             
        PATH = "/opt/maven/bin:$PATH"         
    }                                         
    stages {                                  
        stage("build") {                      
            steps {                           
                echo "----------- build started ----------"
                                              
                sh 'mvn clean deploy'
                                              
                echo "----------- build completed ----------"                                
            }                                 
        }                                     
        stage("Jar Publish") {               
            steps {                           
                script {                      
                    echo '<--------------- Jar Publish Started --------------->'  
                                              
                    def server = Artifactory.newServer url: registry + "/artifactory", credentialsId: "artifact-cred"  
                                              
                    def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}"  
                                              
                    def uploadSpec = """{
                          "files": [
                            {
                              "pattern": "jarstaging/(*)",
                              "target": "koti-libs-release-local/{1}",
                              "flat": "false",
                              "props": "${properties}",
                              "exclusions": [ "*.sha1", "*.md5"]
                            }
                         ]
                     }"""  
                                             
                    def buildInfo = server.upload(uploadSpec)  
                                              
                    buildInfo.env.collect()  
                                              
                    server.publishBuildInfo(buildInfo)  
                                              
                    echo '<--------------- Jar Publish Ended --------------->'  
                                              
                }                             
            }                                 
        }                                     
    }                                         
}                                             

