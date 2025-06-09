pipeline {
  agent any
  stages {
    stage('clonin git repo to custom location') {
      steps {
        dir('/mnt/project') {
          sh 'rm -rf *'
          checkout scm
        }
      }
    }
    stage('creating httpd container') {
      steps {
        sh 'docker run -dp 80:80 --name httpd-1 httpd'
      }
    }
    stage('deploy index.html to container httpd-1') {
      steps {
        dir('/mnt/project') {
          sh 'docker cp index.html httpd-1:/usr/local/apache2/htdocs'
        }
      }
    }
  }
}
