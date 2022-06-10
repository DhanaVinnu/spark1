pipeline {
    agent any 
	    stages  {
		   stage ('git') {
		      steps  {
			    git branch: 'main', credentialsId: 'Dhana', url: 'https://github.com/DhanaVinnu/spark1.git'
				 }
			}
		   stage ('maven') {
			   steps  {
			    bat 'mvn clean install'
				 }
			}
			stage ('nexus') {
			   steps {
				nexusPublisher nexusInstanceId: 'nexus_id',
				nexusRepositoryId: 'maven-snapshots', 
				packages: [
				  [$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: './target/hello-world-war-1.0.0.war']], 
				   mavenCoordinate: [artifactId: 'own_dp', groupId: 'pipeline', packaging: 'war', version: '1.0']
				  ]
				]
                 }
			}
            stage ('tomcat') {
               steps {
                 deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://localhost:8082/')], contextPath: 'pipeline_spark1', war: '**/*.war'
                 }
             }
		}
    }

	 
