pipeline {
  agent any
  stages {
    stage('clonin git repo to custom location') {
      steps {
        dir('/mnt/project2') {
          sh 'rm -rf *'
          checkout scm
        }
      }
    }
    stage('creating httpd container') {
      steps {
        sh 'docker run -dp 8080:80 --name httpd-3 httpd'
      }
    }
    stage('deploy index.html to container httpd-3') {
      steps {
        dir('/mnt/project2') {
          sh 'docker cp index.html httpd-3:/usr/local/apache2/htdocs'
        }
      }
    }
    stage('login to httpd container httpd-3') {
      steps {
        sh 'docker exec httpd-3 bash -c "chmod 777 /usr/local/apache2/htdocs/index.html"'
      }
    }
  }
}
