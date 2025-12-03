pipeline{
	agent any
	stages{
	stage('Build'){
	steps{
	echo "Building Docker Image"
	bat '''
where docker >nul 2>&1
if %errorlevel%==0 (
  docker build -t myfirst .
  exit 0
) else (
  echo Docker not found. Skipping Docker build.
  exit 0
)
'''
	}
	}
	stage('Run'){
	steps{
	echo "Run application in Docker Container"
	bat '''
where docker >nul 2>&1
if %errorlevel%==0 (
  docker rm -f mycontainer 2>nul
  docker run -d -p 5001:5001 --name mycontainer myfirst
  exit 0
) else (
  echo Docker not found. Skipping Docker run.
  exit 0
)
'''
	}
	}
	}
	post{
	success{
	echo 'Pipeline completed successfully!'
	}
	failure{
	echo 'Failed.Please check your logs once again'
	}
	
	}
}
