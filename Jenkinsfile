node('master'){
stage 'Checkout'
	deleteDir()
	checkout scm
stage 'Build'
 	sh 'virtualenv venv; . venv/bin/activate; pip install -r requirements.txt --upgrade'
	sh 'tar -czf build.tar.gz * --exclude Jenkinsfile'
	archiveArtifacts allowEmptyArchive: false, artifacts: 'build.tar.gz', excludes: null, onlyIfSuccessful: true
stage 'Run Tests'
		 sh 'virtualenv venv; . venv/bin/activate; python manage.py test >> resultado.txt'// do something that fails
stage 'Escrevendo'
		sh 'if [ -e resultado.txt  ]; then cat resultado.txt > build.txt; else echo "FALHOU"; fi'
		publishHTML(target: [reportDir: '', reportFiles: 'build.txt', reportName: 'Resultado do Build'])
}
