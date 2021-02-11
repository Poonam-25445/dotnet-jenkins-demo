@Library('SharedLibrary') _
import com.trial.sm.CommonFiles
def commonFile = new CommonFiles()

pipeline {
agent any
 
options {
    skipDefaultCheckout()
}

stages {
stage ('Checkout') {
        steps{
            checkout(scm)
            stash includes: '**', name: 'source', useDefaultExcludes: false
        }
    }
stage ('Restore Packages') {     
         steps {
             deleteDir()
             unstash 'source'
             script {
                 bat '"C:\\Program Files\\dotnet\\dotnet.exe" restore "src\\dotnet-jenkins-demo.sln" '
             }             
          }
        }

stage('Build') {
     steps {
            deleteDir()
            unstash 'source'
            dir('src\\dotnet-jenkins-demo'){
                script{
                    bat '"C:\\Program Files\\dotnet\\dotnet.exe" publish -c release -o /app --no-restore' 
                }
            }
      }
  }
 stage('Prepare Artifacts'){
            steps{
                   echo commonFile.ZipFileName("feature/zipFile","arti")        
            }
        }
  stage('Prepare Artifacts 2'){
            steps{
                   echo artifact.getArtifactFileName("feature/zipFile","arti")       
            }
        }
   }
}

