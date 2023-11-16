pipeline
{
    agent any 
    stages
    {
        stage('Download')
        {
            steps
            {
                git'https://github.com/321ckmdevops/maven.git'
            }
        }
        stage('Build')
        {
            steps
            {
            sh'mvn package'
            }
        }
        stage('Deployment')
        {
            steps
            {
             deploy adapters: [tomcat9(credentialsId: '1d0ee918-382e-4f31-9077-35699c36aeb9', path: '', url: 'http://192.168.29.237:8080')], contextPath: 'ckmtest', war: '**/*.war'
            }
        }
        stage('Testing')
       {
           steps
           {
               git'https://github.com/321ckmdevops/FunctionalTesting.git'
               sh'java -jar /var/lib/jenkins/workspace/CKM_Development_1/testing.jar'
           }
       }
       stage('Delevery')
       {
           steps
           {
               deploy adapters: [tomcat9(credentialsId: '1d0ee918-382e-4f31-9077-35699c36aeb9', path: '', url: 'http://192.168.29.99:8080')], contextPath: 'ckmprod', war: '**/*.war'
           }
       }
       
    }  
}
