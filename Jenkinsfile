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
                scannerHome = tool 'kotidemy-sonarqube-scanner'  
				
            }                                 

            steps {                           
                withSonarQubeEnv('kotidemy-sonarqube-server') {
                                              
                    sh "${scannerHome}/bin/sonarqube-scanner"
                                              
                }                             
            }                                
        }                                     
    }                                         
}               
