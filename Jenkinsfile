pipeline
{
  agent any
  stages
  {
    stage('scm checkout')
    { steps { git branch: 'master', url: 'https://github.com/mewvisudha/maven-project.git' } }

    stage('Code build && Execute Unit Test case')
    { parallel 
     { 
       stage ('Execute Unit Test case')
       { steps { withMaven(jdk: 'LocalJDK', maven: 'LocalMaven')
                { sh 'mvn test' } 
               } 
       }
       
       stage ('Code build')
       { steps 
        { withSonarQubeEnv(credentialsId: 'sonar', installationName: 'sonar')
        
          { withMaven(jdk: 'LocalJDK', maven: 'LocalMaven')     
            { sh 'mvn package sonar:sonar' } } }
            
       }
       
     } 
    }
  }
}
