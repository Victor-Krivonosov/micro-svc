def components = [ 
        'front'            : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "erad-ms-monitoring", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'auth-api'         : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "erad-ms-monitoring", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'log-message'      : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "erad-ms-monitoring", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'todos-api'        : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "erad-ms-monitoring", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'user-api'         : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "erad-ms-monitoring", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
]

pipeline {
    agent {
        label "agent"
    }
    stages {
        stage("Setup parameters") { 
            steps { 
                script { 
                    dynamicParameters = [] 
 
                    components.eachWithIndex { name, component, index -> 
                        dynamicParameters << gitParameter(branchFilter: 'origin' + "${index+1}" + '/(.*)', defaultValue: 'develop', quickFilterEnabled: true, name: 'BRANCH_' + name, type: 'PT_BRANCH_TAG', listSize: '10', useRepository: component.GIT, sortMode: 'ASCENDING') 
                        dynamicParameters << booleanParam(name: 'DEPLOY_' + name, defaultValue: false) 
                        dynamicParameters << booleanParam(name: 'DTRACK_' + name, defaultValue: false, description: "____________________________________________________________________________________________________________") 
                    } 
                     
                    dynamicParameters << choice(name: 'STAND', choices: ['dev', 'test', 'ht', 'external'], description: "Choose STAND for deploy to OKD", defaultValue: "dev") 
                    properties([parameters(dynamicParameters)]) 
 
                } 
            } 
        }
        stage('Deploy') {
             agent {
                docker {
                    image '192.168.0.101:5000/myhelm'
                }
            }
            steps {
                sh "echo 'stage deploy'"
                sh 'pwd'
                sh 'helm upgrade --install front -f front/helm/values.yaml front/helm -n micro'
            }
        }
    }
}