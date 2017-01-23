def docker_image_name='shadowrobot/build-tools:trusty-indigo'
node {
  stage('Checkout'){
    checkout scm
  }
  stage('Build'){
    sh 'export docker_image_name="shadowrobot/build-tools:trusty-indigo"'
    sh 'export toolset_branch="master"'
    sh 'export server_type="local"'
    sh 'export used_modules="check_cache,code_coverage"'
    sh 'export ros_release_name="indigo"'
    sh 'export ubuntu_version_name="trusty"'
    sh "export relative_job_path=${WORKSPACE}"
    sh "export unit_tests_result_dir='${env.relative_job_path}/unit_tests'"
    sh "export coverage_tests_result_dir='${env.relative_job_path}/code_coverage'"
    sh "export remote_shell_script='https://raw.githubusercontent.com/shadow-robot/sr-build-tools/${env.toolset_branch}/bin/sr-run-ci-build.sh'"
    sh "curl -s \$( echo ${env.remote_shell_script} | sed 's/#/%23/g' ) | bash /dev/stdin ${env.toolset_branch} ${env.server_type} ${env.used_modules} ${env.relative_job_path}"
  }
}
