pipeline {
    agent { label 'dotnet_7_node' }
    triggers{ pollSCM(* * * * *) }
    /* insert Declarative Pipeline here */
    stages {
        stage('git repo') {
            steps {
                git branch: 'develop', 
                    url: 'https://github.com/ssardhana/nopCommerce.git'
            }
        }
        stage('build package') {
            steps {
                sh 'dotnet restore src/NopCommerce.sln'
                sh 'dotnet build -c Release src/NopCommerce.sln'
                sh 'dotnet publish -c Release src/Presentation/Nop.Web/Nop.Web.csproj -o publish'
                sh 'mkdir publish/bin publish/logs'
                sh 'zip -r nopCommerce.zip publish'
                archive '**/nopCommerce.zip'
            }
        }

    }
}