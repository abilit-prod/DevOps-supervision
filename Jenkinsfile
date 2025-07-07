pipeline {
    agent any

    environment {
        ANSIBLE_INVENTORY = 'inventory/hosts.ini'
        ANSIBLE_PLAYBOOKS_DIR = 'playbooks'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:abilit-prod/DevOps-supervision.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    sudo apt-get update
                    sudo apt-get install -y ansible
                '''
            }
        }

        stage('Deploy Node Exporter') {
            steps {
                sh "ansible-playbook -i ${ANSIBLE_INVENTORY} ${ANSIBLE_PLAYBOOKS_DIR}/deploy_node_exporter.yml"
            }
        }

        stage('Deploy Prometheus') {
            steps {
                sh "ansible-playbook -i ${ANSIBLE_INVENTORY} ${ANSIBLE_PLAYBOOKS_DIR}/deploy_prometheus.yml"
            }
        }

        stage('Deploy Grafana') {
            steps {
                sh "ansible-playbook -i ${ANSIBLE_INVENTORY} ${ANSIBLE_PLAYBOOKS_DIR}/deploy_grafana.yml"
            }
        }
    }

    post {
        failure {
            echo 'Le pipeline a échoué. Veuillez vérifier les logs.'
        }
        success {
            echo 'Déploiement réussi avec Ansible !'
        }
    }
}
