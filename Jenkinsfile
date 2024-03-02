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
                    dynamicParameters << booleanParam(name: 'DEPLOY_' + name, defaultValue: false), description: "Choose SERVICE for deploy", defaultValue: "") 
                    dynamicParameters << choice(name: 'STAND', choices: ['micro'], description: "Choose STAND for deploy to OKD", defaultValue: "")
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
}
                    sh "echo service1 "+ components.front
                components.each { name, component -> 
                sh """
                helm upgrade --install $helm_release_name \
                --wait \
                --namespace $namespace \
                --set image.tag=$docker_image_tag \
                --set app.standName=$stand_name \
                --set app.buildName=$env.BUILD_DISPLAY_NAME \
                --set image.repository="$DOCKER_REGISTRY" \
                --set image.folder="$IMAGE_FOLDER" \
                $extended_set \
                -f ./ci/helm/$helm_release_name/$helm_var_file \
                ./ci/helm/$helm_release_name
                """
                script { 
                    stagesToExecute = [:] 
                    components.each { name, component -> 
                        COMPONENT_BRANCH = params."BRANCH_$name".replace("/", "-") 
                        HELM_EXTENDED_SET = "--set app.branch=$COMPONENT_BRANCH" 
                        if( params['DEPLOY_'+name] ) { 
                            stagesToExecute[component.HELM_NAME] = common.buildAndDeployHelm(name,component.BUILD_JOB,component.HELM_NAME,"somb-${params.STAND}","${params.STAND}",HELM_VARS_FILE,HELM_EXTENDED_SET) 
                        } 
                    } 
                    if (!stagesToExecute.keySet().isEmpty()) { 
                        parallel(stagesToExecute) 
                    } 
                }
                }
                }
            }
        }
    }
}