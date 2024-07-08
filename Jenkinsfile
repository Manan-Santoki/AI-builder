pipeline {
    agent any

    stages {
        stage('Setup Environment') {
            steps {
                script {
                    // Navigate to the desired directory
                    dir('/root/testing/app') {
                        // Run commands to set up the project
                        sh 'npx create-react-app my-headphone-shop'
                        dir('my-headphone-shop') {
                            // Install dependencies and initialize Tailwind CSS
                            sh 'npm install -D tailwindcss postcss autoprefixer'
                            sh 'npx tailwindcss init -p'
                            
                            // Edit tailwind.config.js file
                            writeFile file: 'tailwind.config.js', text: '''
// tailwind.config.js
module.exports = {
  purge: ['./src/**/*.{js,jsx,ts,tsx}', './public/index.html'],
  darkMode: false,
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
'''
                            // Edit src/App.css file
                            writeFile file: 'src/App.css', text: '''
/* src/App.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
'''
                        }
                    }
                }
            }
        }
        stage('Install Dependencies') {
            sh 'npm i'
        }
        stage('Run code ') {
            sh 'pm2 --name Test1 start npm -- start'
        }

    }
}
