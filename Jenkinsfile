pipeline {
  agent any
  stages {
    stage('clonin git repo to custom location') {
      steps {
        dir('/mnt/project1') {
          sh 'rm -rf *'
          checkout scm
        }
      }
    }
    stage('creating httpd container') {
      steps {
        sh 'docker run -dp 90:80 --name httpd-2 httpd'
      }
    }
    stage('deploy index.html to container httpd-2') {
      steps {
        dir('/mnt/project1') {
          sh 'docker cp index.html httpd-2:/usr/local/apache2/htdocs'
        }
      }
    }
    stage('login to httpd container httpd-2') {
      steps {
        sh 'docker exec httpd-2 bash -c "chmod 777 /usr/local/apache2/htdocs/index.html"'
      }
    }
  }
}
