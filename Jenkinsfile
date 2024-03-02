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
                     
                    dynamicParameters << choice(name: 'STAND', choices: ['dev', 'test', 'ht', 'external'], description: "Choose STAND for deploy to OKD", defaultValue: "dev") 
                    properties([parameters(dynamicParameters)]) 
                } 
            } 
        }
        stage('Deploy') {
            //  agent {
            //     docker {
            //         image '192.168.0.101:5000/myhelm'
            //     }
            // }
            steps {
                script { 
                components.each { name, component -> 
                if( params['DEPLOY__'+name] ) {
                sh 'echo Start Deploy:  '+component.HELM_NAME

                sh """
                helm_release_name=component.HELM_NAME
                #echo "\$helm_release_name"
                #    helm upgrade --install $helm_release_name \
                #    --wait \
                #    --namespace $namespace \
                #    -f ./ci/helm/$helm_release_name/$helm_var_file \
                #    ./ci/helm/$helm_release_name
                """
                }
                }
            }
        }
    }
}
}