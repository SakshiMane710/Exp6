index.html -- style.css -- script.js

git init
git add .
git commit -m "Initial web application"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/Exp6-CICD-WebApp.git
git push -u origin main


jenkin ---name ---- pipeline --- Pipeline script

-------------------------------------------------------------------------------------------


pipeline {
    agent any

  stages {

  stage('Checkout') {
            steps {
                echo 'Downloading project from GitHub'

  git branch: 'main',
                    url: 'https://github.com/SakshiMane710/Exp6.git'
            }
        }

  stage('Build') {
            steps {
                echo 'Building Web Application'

  bat 'dir'
                echo 'Build completed successfully'
            }
        }

       
stage('Test') {
    steps {
        echo 'Testing HTML file'

   bat '''
        if not exist index.html exit /b 1
        findstr /I "<html>" index.html
        if errorlevel 1 exit /b 1
        echo HTML file validation successful
        '''
    }
}


  stage('Deploy') {
            steps {
                echo 'Deploying website'

  bat '''
                if not exist "C:\\inetpub\\wwwroot\\Exp6" mkdir "C:\\inetpub\\wwwroot\\Exp6"
                xcopy /E /I /Y * "C:\\inetpub\\wwwroot\\Exp6\\"
                '''

  echo 'Deployment completed successfully'
            }
        }
    }

  post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

  failure {
            echo 'Pipeline failed! Check Console Output.'
        }
    }
}

-----------------------------------------------------------------------------------------------

configure -- trigger -- Poll SCM -- H/2 * * * *

verify deployment  http://localhost/Exp6/index.html

------------------------------------------------------------------------------------------------

win + R ---  optionalfeatures  ---

Web Management Tools
- IIS Management Console


World Wide Web Services
- Common HTTP Features
  - Static Content
  - Default Document
