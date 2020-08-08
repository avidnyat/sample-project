pipeline {
    agent any

    stages {
        stage('Environment Setup') {
            stages {
               stage("Install Pre-requisites") {
                   steps {
                      echo "Installing pre-requisites"
                      sh "sudo ansible-playbook /root/ansible-project/ansible-playbooks/lamp_ubuntu1804/prerequisite.yml -l web_server -u root"
                   }
               }
               stage("Install LAMP") {
                   steps {
                      echo "Installing LAMP Packages"
                      sh "sudo ansible-playbook /root/ansible-project/ansible-playbooks/lamp_ubuntu1804/install-lamp.yml -l web_server -u root"
                   }
               }
               stage("Enable Apache Configuration") {
                   steps {
                      echo "Configuring Virtual host"
                      sh "sudo ansible-playbook /root/ansible-project/ansible-playbooks/lamp_ubuntu1804/apache-enable-site.yml -l web_server -u root"
                   }
               }
               stage("Expose Port 80") {
                   steps {
                      echo "Allowing Port 80"
                      sh "sudo ansible-playbook /root/ansible-project/ansible-playbooks/lamp_ubuntu1804/expose-port.yml -l web_server -u root"
                   }
               }
            }
        }
        stage('Build setup') {
            stages {
                stage("Taking backup") {
                   steps {
                       sh 'sudo ansible-playbook /root/ansible-project/ansible-playbooks/lamp_ubuntu1804/build-number.yml -l web_server -u root --extra-vars 'version= ${env.BUILD_NUMBER}''
                   }
                }
                stage("Git new clone") {
                   steps {
                       echo 'Git Clone'
                       sh "sudo ansible-playbook /root/ansible-project/ansible-playbooks/lamp_ubuntu1804/git-clone.yml -l web_server -u root"
                   }
                }
                stage("composer install") {
                   steps {
                       echo 'composer install done'
                   }
                }
                stage("Create Artifact") {
                   steps {
                       echo 'Create Artiface'
                   }
                }
            }
        }
    }
}
