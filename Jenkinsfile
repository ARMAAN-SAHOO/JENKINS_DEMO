pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'feature-demo', description: 'Branch name to create')
    }

    environment {
        GITHUB_TOKEN = credentials('GITHUB_TOKEN') // Jenkins secret text
        REPO = 'ARMAAN-SAHOO/JENKINS_DEMO'           // Replace with your GitHub repo
    }

    stages {

        stage('Clone Repo') {
            steps {
                sh """
                git clone https://${GITHUB_TOKEN}@github.com/${REPO}.git repo
                """
            }
        }

        stage('Create Branch') {
            steps {
                dir('repo') {
                    // Create new branch or reset if it exists
                    sh "git checkout -B ${params.BRANCH_NAME}"
                }
            }
        }

        stage('Make Change') {
            steps {
                dir('repo') {
                    sh """
                    echo "Test change from Jenkins" >> test.txt
                    git add .
                    git commit -m "Change from Jenkins pipeline" || echo "No changes to commit"
                    """
                }
            }
        }

        stage('Push Branch') {
            steps {
                dir('repo') {
                    sh "git push -u origin ${params.BRANCH_NAME}"
                }
            }
        }

        stage('Create Pull Request') {
            steps {
                sh """
                curl -s -X POST \
                -H "Authorization: token ${GITHUB_TOKEN}" \
                -H "Accept: application/vnd.github+json" \
                https://api.github.com/repos/${REPO}/pulls \
                -d '{"title":"Merge ${params.BRANCH_NAME} into main","head":"${params.BRANCH_NAME}","base":"main"}'
                """
            }
        }

    }
}


/*
                    // git config user.name "ARMAAN-SAHOO"
                    // git config user.email "armaansahoo6@gmail.com"
*/