node {
  properties([
    parameters([
      booleanParam (name: 'buildImage', defaultValue: false, description: 'Build new docker image')
    ])
  ])

  checkout scm

  stage('Docker image') {
    if (params.buildImage) {
      docker.withRegistry('https://docker.big-xyt.com', 'tu_deploy') {
        def img = docker.build('minio')
        // Git commit hash is not available by default, hence the workaround
        sh 'git rev-parse HEAD > commit'
        img.push(readFile('commit').trim())
        sh "docker rmi ${img.id}"
      }      
    }
  }
}
