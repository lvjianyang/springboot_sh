node{
    stage('git clone'){
        //check out
        //git credentialsId: '62420ea8-44cd-4657-98fa-6e07f0901957', url: 'https://github.com/lvjianyang/springboot_sh.git'
		checkout scm
    }

    stage('build'){
        docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2'){
            sh 'mvn package -B -DskipTests'
        }
		def testImage = docker.build("test-springboot", "-f docker/Dockerfile .") 

		docker.image('test-springboot:latest').withRun('-p 8088:8088') {
           sh 'echo finish!'
        }
    }
}