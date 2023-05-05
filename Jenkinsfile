node {
    docker.image('maven:3.9.0-eclipse-temurin-11').inside('-v /root/.m2:/root/.m2'){
        stage("Build") {
            sh 'mvn -B -DskipTests clean package'
        }
        stage("Test") {
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
        stage("Manual Approval") {
            input message: 'Apakah ingin melanjutkan ke tahap Deploy? (Klik "Proceed" untuk melanjutkan)' 
        }
        stage("Deploy") {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan Maven App? (Klik "Proceed" untuk mengakhiri)' 
            sleep(time: 1, unit: 'MINUTES')
        }
    }
}