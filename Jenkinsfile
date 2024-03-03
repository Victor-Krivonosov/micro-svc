def components = [ 
        'front'            : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "front", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'auth-api'         : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "auth-api", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'log-message'      : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "log-message", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'todos-api'        : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "todos-api", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
        'user-api'         : ["BUILD_JOB": "NDR_WO/build/erad_ms_monitoring", "HELM_NAME": "user-api", "GIT": "https://github.com/Victor-Krivonosov/micro-svc.git"],
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
                    dynamicParameters << booleanParam(name: 'DEPLOY__' + name, defaultValue: false, description: "____________________________________________________________________________________________________________") 
                    } 
                     
                    dynamicParameters << choice(name: 'STAND', choices: ['micro'], description: "Choose STAND for deploy", defaultValue: "micro") 
                    properties([parameters(dynamicParameters)]) 
                } 
            } 
        }
        stage('Deploy') {
             agent {
                docker {
                    image '192.168.0.101:5000/myhelm2'
                }
            }
            // environment { 
            //     namespace = "${STAND}"
            //     }

            steps {
                script { 
                sh 'echo Start Deploy: '
                // components.each { name, component -> 
                // if( params['DEPLOY__'+name] ) {
                // helm_release_name = component.HELM_NAME
                // sh 'echo Start Deploy:  '+component.HELM_NAME
                // sh 'echo \$helm_release_name'
                // sh """
                
                // echo "\$helm_release_name"
                //     helm upgrade --install $helm_release_name \
                //     --wait \
                //     --namespace $namespace \
                //     -f ./$helm_release_name/helm/values.yaml \
                //     ./$helm_release_name/helm
                // """
                }
                }
            }
        }
    }
// }
// }