def mapOfStages = [:]

mapOfStages["hello"] = {
    stage ('Say hello') {
        echo "hello"
    }
}

def dockerImages = ["gradle:jdk8","gradle:jdk11","gradle:jdk13"]
dockerImages.each {
    mapOfStages["${it}"] = { 
        docker.image("${it}").inside {
            stage("${it}") {
                git branch: 'master', url: 'https://github.com/praqma-training/jenkins-katas.git'
                sh 'ci/build-app.sh'
                archiveArtifacts 'app/build/libs/'
            }
        }
    }
}

node { 
    stage('Parallel stuff') {
        parallel mapOfStages
    }
}