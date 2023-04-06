def versionpython= ["python3.8", "python3.9"]

 
pipeline {
  agent none
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
    timeout(time: 60, unit:'MINUTES')
    timestamps()
  }
  stages {
    stage("install requirements Python"){
	  agent { label 'slave_d1' }
      steps{
        script{
	        versionpython.each {item ->
			    withPythonEnv("/usr/bin/${item}") {
					stage("install requirement") {
						steps{
							sh "python --version"
							sh "pip --version"
							sh "pip install -r requirements.txt"
							sh 'python -m py_compile sources/add2vals.py sources/calc.py'
							sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
						}
					}
			    }
	        }
		}
      }
    }

  }
}