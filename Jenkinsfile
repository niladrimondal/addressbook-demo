pipeline {
    agent any
    tools{
        maven 'mvn1'
    }

    stages {
        stage('Checkout the Source Code') {
            steps {
                echo 'Checkout the code..........................................'
                git 'https://github.com/niladrimondal/addressbook-demo.git'
            }
        }
        stage('Build The Source Code') {
            steps{
			    script{
				     try{
                       echo 'Build the Source Code ....................................'
                       sh "mvn clean package"
					 }
					 catch(Exception e){
                         echo 'handling the exception ...................................'
                         emailext body: '''Hello Developer,

                         The Job got failed during Build.

                         Thanks,
                         Devops''', subject: 'Attention: $(JOB_NAME) is failed. Please look into the Build Number $(BUILD_NUMBER)', to: 'niladrimondal.mondal@gmail.com'
                    }
				
				}
                
            }
        }
        stage('Deploy the Application') {
            steps {
                echo 'Deploy the Application.....................................'
                deploy adapters: [tomcat9(credentialsId: 'tomcat-cred', path: '', url: 'http://54.158.200.34:8081/')], contextPath: 'addressbookssimplilearn', war: '**/*.war'
            }
        }
    }
}
