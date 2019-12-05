https://www.cnblogs.com/zhuyan521/p/10791121.html
https://blog.csdn.net/wenwenxiong/article/details/78953242

导航到jenkins>管理jenkins>进程内脚本批准

有一个挂起的命令，批准。


此版本采用jenkins2
1 容器方式运行jenkins
2 写dockfile脚本
3 写pipeline脚本
  node{
    stage('git clone'){
		checkout scm
    }

    stage('build'){
        docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2'){
            sh 'mvn package -B -DskipTests'
        }
		def testImage = docker.build("test-springboot", "-f docker/Dockerfile .") 
		
    }
	
	stage('deploy images'){
		sh 'docker rm  -f  `docker ps -aq --filter name=springboot` | true'
		sh 'docker run -d -p 8088:8088 --name springboot test-springboot'

    }
}
4 运行后访问http://192.168.163.130:8088/hello

