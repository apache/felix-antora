pipeline {
    agent {
            label 'git-websites'
    }

    stages {
        stage('build') {
            steps {
                sh 'rm -rf build'
// clone the felix-site-pub repo
                sh 'git clone --depth 1 --branch asf-site https://gitbox.apache.org/repos/asf/felix-site-pub.git build/site'
                dir('build/site') {
                    sh 'git rm -r .'
                }

                sh 'npm run plain-install'
                sh 'npm run build-noclean'

                dir('build/site') {
		          sh 'git add .'
		          sh 'echo `git commit -m "site build"`'
//                  sh 'git push https://gitbox.apache.org/repos/asf/felix-site-pub.git asf-site'
		}
            }
        }
    }
}