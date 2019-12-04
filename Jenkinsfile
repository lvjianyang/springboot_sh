node{
    stage('git clone'){
        //check out
        git credentialsId: '62420ea8-44cd-4657-98fa-6e07f0901957', url: 'https://github.com/lvjianyang/springboot_sh.git'
    }

    stage('build'){
        docker.image('maven-alpine').inside{
            sh 'mvn package -B -DskipTests'
        }
    }
}