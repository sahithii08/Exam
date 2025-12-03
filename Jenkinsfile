pipeline{
	agent any
	stages{
	stage('Build'){
	steps{
	echo "Building Docker Image"
	bat "docker build -t myfirst "
	}
	}
	stage('Run'){
	steps{
	echo "Run application in Docker Container"
	bat "docker rm -f mycontainer || exit 0"
	bat "docker run -d -p 5001:5001 --name mycontainer myfirst"
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
