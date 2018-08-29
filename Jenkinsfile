def label = "buildpod.${env.JOB_NAME}.${env.BUILD_NUMBER}".replace('-', '_').replace('/', '_')
podTemplate(label: label, containers: [
    containerTemplate(name: 'step-0-0', image: 'rancher/alpine-git:1.0.4', ttyEnabled: true, command: 'cat' ),
	containerTemplate(name: 'step-1-0', image: 'busybox:latest', ttyEnabled: true, command: 'cat' , envVars: [
		envVar(key: 'CICD_GIT_REPO_NAME', value: 'php-test'),
		envVar(key: 'CICD_PIPELINE_ID', value: 'p-gzszp:p-7hw57'),
		envVar(key: 'CICD_EXECUTION_SEQUENCE', value: '2'),
		envVar(key: 'CICD_GIT_COMMIT', value: 'fee5fdf'),
		envVar(key: 'CICD_GIT_BRANCH', value: 'refs/heads/master'),
		envVar(key: 'CICD_GIT_URL', value: 'https://github.com/heamaral/php-test.git'),
		envVar(key: 'CICD_PIPELINE_NAME', value: 'pipeline-php-test'),
		envVar(key: 'CICD_TRIGGER_TYPE', value: 'webhook'),
		envVar(key: 'CICD_EXECUTION_ID', value: 'p-gzszp:p-7hw57-2'),
	]),
	containerTemplate(name: 'jnlp', image: 'rancher/jenkins-jnlp-slave:3.10-1-alpine', args: '${computer.jnlpmac} ${computer.name}', ttyEnabled: false, envVars: [
		envVar(key: 'JENKINS_URL', value: 'http://jenkins:8080')
	])
]) {
	node(label){
	    timestamps {

            stage('clone') {
                parallel 'step-0-0': {
                  stage('step-0-0'){
                    container(name: 'step-0-0') {
                      checkout scm
                    }
                  }
                }
            }

            stage('build') {
                parallel 'step-1-0': {
                  stage('step-1-0'){
                    container(name: 'step-1-0') {
                        sh ''' ls '''
                    }
                  }
                }
    		}
            
	    }
	}
}