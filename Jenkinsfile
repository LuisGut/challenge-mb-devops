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
    stage('Checkout') {
      steps {
        checkout scm
      }
    }  
    stage('Install Packages') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test and Build') {
      parallel {
        stage('Run Tests') {
          steps {
            sh 'npm run test'
          }
        }
        stage('Create Build Artifacts') {
          steps {
            sh 'npm run build'
          }
        }
      }
    }
  }
}   