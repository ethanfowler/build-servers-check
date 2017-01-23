def docker_image_name='shadowrobot/build-tools:trusty-indigo'
node {
  stage('Checkout'){
    checkout scm
  }
  stage('Build'){
  sh """#!/bin/bash -l
    export docker_image_name="shadowrobot/build-tools:trusty-indigo"
    export toolset_branch="master"
    export server_type="local"
    export used_modules="check_cache,code_coverage"
    export ros_release_name="indigo"
    export ubuntu_version_name="trusty"

    export relative_job_path=\${${WORKSPACE}#$HOME}

    export unit_tests_result_dir="\$relative_job_path/unit_tests"
    export coverage_tests_result_dir="\$relative_job_path/code_coverage"

    export remote_shell_script="https://raw.githubusercontent.com/shadow-robot/sr-build-tools/$toolset_branch/bin/sr-run-ci-build.sh"
    curl -s "\$( echo "$remote_shell_script" | sed 's/#/%23/g' )" | bash /dev/stdin "$toolset_branch" $server_type $used_modules $relative_job_path
  """
  }
}
