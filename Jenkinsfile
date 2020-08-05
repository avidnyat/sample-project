pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Install apache2'
                sh "sudo ansible-playbook /root/ansible-project/ansible-playbooks/lamp_ubuntu1804/playbook.yml -l web_server -u root"
                echo "Lamp stack installed"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
