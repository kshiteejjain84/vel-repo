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
    stage('deleting old containers') {
      steps {
        sh 'docker kill \$(docker ps -q) || true'
        sh 'docker system prune -a -f'
      }
    }
    stage('creating httpd container') {
      steps {
        sh 'docker run -dp 90:80 --name httpd-2 httpd'
      }
    }
    stage('deploy index.html to container httpd-2') {
      steps {
        dir('/mnt/project') {
          sh 'docker cp index.html httpd-1:/usr/local/apache2/htdocs'
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
