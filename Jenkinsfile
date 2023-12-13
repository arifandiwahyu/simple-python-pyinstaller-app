node {
    stage('Build') {
        withDockerContainer(image: 'python:3.12.1-alpine3.19') {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            stash name: 'compiled-results', includes: 'sources/*.py*'
        }
    }
    try {
        stage('Test') {
            withDockerContainer(image: 'qnib/pytest') {
                sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
            }
        }
    } finally {
                junit 'test-reports/results.xml'
            }
    }

