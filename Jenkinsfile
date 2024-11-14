pipeline
{
    agent any
    stages
    {
        stage('contdownload')
        {
            steps
            {
               git 'https://github.com/vamsi-chinnodu/maven.git' 
            }
        }
        stage('contbuild')
        {
            steps
            {
              sh 'mvn package'

            }
        }
        stage('contdeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: '4a534462-3c1c-4319-b8cf-e5ad4e9cd0c5', path: '', url: 'http://172.31.20.116:8080')], contextPath: 'newtestapp', war: '**/*.war' 
            }
        }
        stage('conttesting')
        {
            steps
            {
               git 'https://github.com/vamsi-chinnodu/FunctionalTesting.git' 
               sh 'java -jar /var/lib/jenkins/workspace/Declarativepipeline/testing.jar'

            }
        }
        stage('cont delivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '94f0cdd7-ac28-4297-8c9d-b9a4918b7c75', path: '', url: 'http://172.31.25.203:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
       
    }   
    
}
