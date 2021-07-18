//these don't seem to work.
//def siteBranch = "asf-site"
//def siteBranch = "asf-staging"

pipeline {
    agent {
            label 'git-websites'
    }

    stages {
        stage('build') {
            steps {
                sh 'rm -rf build'
// clone the felix-site-pub repo
                sh 'git clone --depth 1 --branch asf-staging https://gitbox.apache.org/repos/asf/felix-site-pub.git build/site'
                dir('build/site') {
                    sh 'git rm -r .'
                }

                sh 'npm run clean-install'
                sh 'ls ./node_modules/@apache-felix'
                sh 'ls ./node_modules/@apache-felix/felix-antora-ui'
                sh 'ls ./node_modules/@apache-felix/felix-antora-ui/build'
                sh 'ls ./node_modules/@apache-felix/felix-antora-ui/build/felix-antora-ui-bundle.zip'
                sh 'npm run build-noclean'

                dir('build/site') {
		          sh 'git add .'
		          sh 'echo `git commit -m "site build"`'
                  sh 'git push https://gitbox.apache.org/repos/asf/felix-site-pub.git asf-staging'
	        	}
            }
        }
    }
}