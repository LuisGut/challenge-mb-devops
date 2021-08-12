pipeline {
  agent any
  tools { 
    nodejs "mynode" 
  }
  
  environment {
    CI = 'true'
    HOME = '.'
    PATH="$PATH:${pwd()}/.npm-global/bin:${pwd tmp: true}/.npm-global/bin"
    npm_config_cache = 'npm-cache'
  }
  
  stages {  
    stage('Install Packages') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
          steps {
            sh 'npm run build'
          }
    }
    stage('Deployment') {
          steps {
            withAWS(region:'us-east-1',credentials:'test-user') {
              s3Delete(bucket: 'challengebmusic', path:'**/*')
              s3Upload(bucket: 'challengebmusic', workingDir:'build', includePathPattern:'**/*');
            }
          }
        }
  }
}
   