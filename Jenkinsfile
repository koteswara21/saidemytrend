pipeline {                                    // 1  // Defines the start of the Jenkins pipeline block

    agent any                                 // Specifies the pipeline can run on any available agent

    environment {                             // 2  // Defines environment variables for the pipeline
        PATH = "/opt/maven/bin:$PATH"         // Adds Maven's path to the system's PATH variable
    }                                         // 2  // Ends the environment block

    stages {                                  // 3  // Defines the stages block where multiple stages are declared

        stage("build") {                      // 4  // Creates a stage named 'build'
            steps {                           // 5  // Defines the steps that will be executed in this stage
                echo "----------- build started ----------"
                                              // Logs a message indicating the start of the build
                sh 'mvn clean deploy'
                                              // Runs Maven clean and deploy commands, skipping tests
                echo "----------- build completed ----------"
                                              // Logs a message indicating the build completion
            }                                 // 5  // Ends the steps block for 'build' stage
        }                                     // 4  // Ends the 'build' stage

        stage('SonarQube analysis') {         // 8  // Creates a stage named 'SonarQube analysis'
            environment {                     // 9  // Defines environment variables specific to this stage
                scannerHome = tool 'kotidemy-sonar-scanner'
                                              // Sets the SonarQube scanner tool
            }                                 // 9  // Ends the environment block for this stage

            steps {                           // 10  // Defines the steps that will be executed in this stage
                withSonarQubeEnv('kotidemy-sonarqube-server') {
                                              // Executes the SonarQube analysis within the SonarQube environment
                    sh "${scannerHome}/bin/sonar-scanner"
                                              
                }                             
            }                                 // 10  // Ends the steps block for 'SonarQube analysis' stage
        }                                     // 8  // Ends the 'SonarQube analysis' stage
    }                                         // 3  // Ends the stages block
}                                             // 1  // Ends the pipeline block

