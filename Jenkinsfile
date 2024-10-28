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
        stage('SonarQube analysis') {         
            environment {                     
                scannerHome = tool 'saidemy-sonar-scanner'  	
            }                                 
            steps {                           
                withSonarQubeEnv('saidemy-sonar-server') {
                                              
                    sh "${scannerHome}/bin/sonar-scanner" 				
                }                             
            }                                
        } 
        stage("Quality Gate") {               
            steps {                           
                script {                      
                    timeout(time: 1, unit: 'HOURS') {
                                              
                        def qg = waitForQualityGate()
                                              
                        if (qg.status != 'OK') {
                                              
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }                                         
}
