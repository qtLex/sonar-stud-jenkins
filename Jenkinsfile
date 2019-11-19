pipeline {
    parameters {
        string(defaultValue: "${env.jenkinsAgent}", description: 'Нода дженкинса, на которой запускать пайплайн. По умолчанию master', name: 'jenkinsAgent')
    }

    agent {
        label "${(env.jenkinsAgent == null || env.jenkinsAgent == 'null') ? "master" : env.jenkinsAgent}"
    }

    options {
        timeout(time: 8, unit: 'HOURS')
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage("Подготовка конфигурации к анализу") {
            steps {
                timestamps {
                    script {
                        cmd("runner init-dev --ibconnection /F./db.work --v8version 8.3.15.1747 --dt C:\\Users\\ived\\students\\ived_20191119_1.dt")
                        cmd("runner decompile --ibconnection /F./db.work --v8version 8.3.15.1747 --out ./cf")
                    }
                }
            }
        }
    }
}

def cmd(command) {
    // при запуске Jenkins не в режиме UTF-8 нужно написать chcp 1251 вместо chcp 65001
    if (isUnix()) { sh "${command}" } else { bat "chcp 65001\n${command}" }
}