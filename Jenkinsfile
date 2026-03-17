pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'feature-demo', description: 'Branch name to create')
    }

    environment {
        GITHUB_TOKEN = credentials('GITHUB_TOKEN')
        REPO = 'ARMAAN-SAHOO/JENKINS_DEMO'
    }

    stages {

        stage('Clone Repo') {
            steps {
                bat """
                git clone https://%GITHUB_TOKEN%@github.com/%REPO%.git repo
                """
            }
        }

        stage('Create Branch') {
            steps {
                dir('repo') {
                    bat "git checkout -B %BRANCH_NAME%"
                }
            }
        }

        stage('Make Change') {
            steps {
                dir('repo') {
                    bat """
                    git config user.name "Jenkins Bot"
                    git config user.email "jenkins@demo.com"

                    echo Test change from Jenkins >> test.txt
                    git add .
                    git commit -m "Change from Jenkins pipeline" || echo No changes to commit
                    """
                }
            }
        }

        stage('Push Branch') {
            steps {
                dir('repo') {
                    bat "git push -u origin %BRANCH_NAME%"
                }
            }
        }

        stage('Create Pull Request') {
            steps {
                bat """
                curl -X POST -H "Authorization: token %GITHUB_TOKEN%" -H "Accept: application/vnd.github+json" https://api.github.com/repos/%REPO%/pulls -d "{\\"title\\":\\"Merge %BRANCH_NAME% into main\\",\\"head\\":\\"%BRANCH_NAME%\\",\\"base\\":\\"main\\"}"
                """
            }
        }

    }
}