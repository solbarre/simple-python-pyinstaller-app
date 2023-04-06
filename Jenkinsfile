def versionpython= ["python3.8", "python3.9"]

 
pipeline {
  agent none
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
    timeout(time: 60, unit:'MINUTES')
    timestamps()
  }
  stages {
    stage("checkout projet python") {
        agent { label 'slave_d1' }
		steps{
			script{
				git branch: 'master', url: 'https://github.com/solbarre/simple-python-pyinstaller-app.git'
				sh "ls -lart ./*"
			}
        }
	}
    stage("install requirements Python"){
	  agent { label 'slave_d1' }
      steps{
        script{
	        versionpython.each {item ->
			    withPythonEnv("/usr/bin/${item}") {
			        script {
				        sh "python --version"
				        sh "pip --version"
				        sh "pip install -r requirements.txt"
				    }
			    }
	        }
		}
      }
    }
	stage("compilation") {
	    agent { label 'slave_d1' }
	    steps{
			sh 'python -m py_compile sources/add2vals.py sources/calc.py'
		}
	}
  }
}