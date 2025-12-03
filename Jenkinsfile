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
) else (
  echo Docker CLI not found on PATH. Skipping docker build.
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
  docker rm -f mycontainer 2>nul || echo no container to remove
  docker run -d -p 5001:5001 --name mycontainer myfirst
) else (
  echo Docker CLI not found on PATH. Skipping run stage.
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
