pipeline
{
    agent
    {
        label 'maven'
    }
    tools
    {
        maven 'mvn-3.9.5'
    }
    stages
    {
        stage('SCM-Checkout')
        {
            steps
            {
                checkout scmGit(branches: [[name: 'master']],
                userRemoteConfigs: [
                    [ url: 'https://github.com/JenkinsDeclarativePipeline/second-maven-project.git' ]
                ])
            }
        }
        stage("Maven-Build")
        {
            steps
            {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube analysis') {
        // performing sonarqube analysis with "withSonarQubeENV(<Name of Server configured in Jenkins>)"
        withSonarQubeEnv('sonar-9.9.2') 
        {
        // requires SonarQube Scanner for Maven 3.2+
            sh 'mvn sonar:sonar \
            -Dsonar.projectKey=maven-project \
            -Dsonar.host.url=http://13.239.5.214:9000 \
            -Dsonar.login=sqp_5a5a5ab5c37e4393ba8864f847d3e63bfa4f6be4'
        }
    }
}
