node{
    stage('git clone'){
		checkout scm
    }

    stage('build'){
        docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2'){
            sh 'mvn package -B -DskipTests'
        }
		def testImage = docker.build("test-springboot", "-f docker/Dockerfile .") 
		testImage.inside {
			sh 'cd docker'
			sh 'docker-compose down'       
			sh 'docker-compose up -d'
		}
    }
	
	stage('deploy images'){
		
		sh 'echo finish'
    }
}