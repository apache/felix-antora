// preview branch copy.
// Deploys to asf-staging, which is shown at https://felix.staged.apache.org.

//Set the desired content sources in antora-playbook.yml on this branch:
// these will typically include branches in your forks of the felix github repos.
// Trigger the site build manually with the Jenkins https://ci-builds.apache.org/job/Felix/job/website-build-preview/ action.

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