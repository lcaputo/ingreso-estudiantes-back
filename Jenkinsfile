pipeline{
    agent any
    tools {
        nodejs 'Node LTS 18.17.1'
    }
    environment {
        DB_HOST = credentials('DB_HOST')
        DB_PORT = credentials('DB_PORT')
        DB_NAME = credentials('DB_NAME')
        DB_USER = credentials('DB_USER')
        DB_PASS = credentials('DB_PASS')
    }
    stages{
    	stage("Export secrets"){
            steps{
                script {
                    sh 'export DB_HOST=${DB_HOST}'
                    sh 'export DB_PORT=${DB_PORT}'
                    sh 'export DB_NAME=${DB_NAME}'
                    sh 'export DB_USER=${DB_USER}'
                    sh 'export DB_PASS=${DB_PASS}'
                }
            }
        }
        stage("Build"){
            steps{
                script {
                    sh 'npm i'
                    sh 'npm run build'
                }
            }
        }
        stage("Replace files"){
            steps{
                script {
                    sh 'rm -rf ~/home/api/*'
                    sh 'cp -r ./dist/* ~/home/api/'
                }
            }
        }
    }
}