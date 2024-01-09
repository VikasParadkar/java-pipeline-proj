pipeline
{
    agent any
    tools
    {
        maven 'maven'
    }
    
    stages
    {
        stage ('SCM')
        {
            steps
            { 
                echo "starting with the SCM steps"
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/qmetry/junit-java-example.git']])
                echo "The Ssource code has been checked out"
            }
        }
        
        stage ('BUILD')
        {
            steps
            {
                echo "starting with the build steps"
                sh 'mvn compile'
            }
        }
        
        stage ('TEST')
        {
            steps
            {
                echo "starting with the test"
                sh 'mvn test'
				junit 'target/surefire-reports/**.xml'
				jacoco exclusionPattern: '**/*Test*.class', execPattern: '**/target/**.exec,', inclusionPattern: '**/*.class', sourceInclusionPattern: '**/*.java', sourcePattern: 'target/src/main/java'
            }
        }
        
        stage ('DEPLOY')
        {
            steps
            {
                echo "starting with deploy"
                sh 'mvn install'
            }
        }
    
    }
}
