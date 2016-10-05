
stage 'Checkout'
	node('master'){
	deleteDir()
	checkout scm
}
stage 'Build'
 node('master') {
 sh 'export WORKSPACE=pwd; virtualenv venv; source venv/bin/activate; pip install -r requirements.txt'
  step([$class: 'ArtifactArchiver', artifacts: '/workspace/venv/'])
}
stage 'Run Tests'
  node('master') {
   sh 'python manage.py test'
   publishHTML(target: [reportDir: 'build/reports/teste', reportFiles: 'index.html', reportName: 'Testes Instrumentados'])
   step([$class: 'JUnitResultArchiver', testResults: 'build/outputs/connected/*.xml'])
}
