def testType = ['Load', 'Stress', 'Endurance']
pipeline {
    agent any
    parameters {
        choice(name: 'TestType', choices: testType, description: 'Test types')
    }
    options { disableConcurrentBuilds() }
stages {
        stage('Init') {
            steps {
                echo "Remove old data"
                bat 'rmdir /Q /S "C:\\Work\\apache-jmeter-5.4.1\\results"'
                bat 'mkdir "C:\\Work\\apache-jmeter-5.4.1\\results"'
                bat 'del /F /Q "C:\\Work\\apache-jmeter-5.4.1\\test.jtl"'
            }
        }
        
        stage('Run JMeter') {
            steps {
              bat "C:/Work/apache-jmeter-5.4.1/apache-jmeter-5.4.1/bin/jmeter.bat -n -t C:/Work/apache-jmeter-5.4.1/test.jmx -l C:/Work/apache-jmeter-5.4.1/test.jtl -j C:/Work/apache-jmeter-5.4.1/test.log -e -o C:/Work/apache-jmeter-5.4.1/results -Jthreads=${params.NumberofUsers}"
            }
        }
        
        stage('Results') {
            steps {
              bat 'copy "C:\\Work\\apache-jmeter-5.4.1\\test.*" .'
              archiveArtifacts "test.*"
            }
        }
}
}