pipeline {
    agent any

    stages {
        stage('Clear files') {
            steps {
                sh 'sudo rm -rf /root/testing/app'
                sh 'sudo mkdir -p /root/testing/app'
            }
        }
        stage('Create Template') {
            steps {
                dir('/root/testing/app'){
                script {
                    sh '''
                    sudo npx create-react-app my-headphone-shop && cd my-headphone-shop'''
                    sh '''
                    sudo npm install -D tailwindcss postcss autoprefixer && sudo npx tailwindcss init -p
                    '''
                    sh '''
                    sudo cat << EOF > tailwind.config.js
                    module.exports = {
                      content: [
                        "./src//*.{js,jsx,ts,tsx}",
                      ],
                      theme: {
                        extend: {},
                          },
                     plugins: [],
                    }
                    EOF    '''
                    sh '''
                    sudo cat << EOF >> src/index.css
                    @tailwind base;
                    @tailwind components;
                    @tailwind utilities;
                    EOF

                    '''

                    }
                }

            }
        }
        stage('Edit Files') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }
    }
}