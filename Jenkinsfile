pipeline {
    agent any
    // 병렬처리의 대상이 되는 Job를 선언
    // 모든 변수에 기본 값을 넣어 주었습니다.
    parameters {
        string(
            name: 'Step_01',
            defaultValue: "my_pipeline"
        )
        string(
            name: 'Step_02',
            defaultValue: "PipelineTest02"
        )
        string(
            name: 'Step_03',
            defaultValue: "PipelineTest03"
        )
    }
    stages {
        stage('parallel build') {
            steps {
                // steps 단계를 병렬처리
                // 각각의 Job은 동시에 빌드 됩니다.
                parallel(
                    "First_Step": {
                        echo "${params.Step_01}"
                        build "${params.Step_01}"
                    },
                    "Second_Step": {
                        echo "${params.Step_02}"
                        build "${params.Step_02}"
                    },
                    "Third_Step": {
                        echo "${params.Step_03}"
                        build(
                            job: "${params.Step_03}",
                            parameters: [
                                text(name: 'FILE_NAME', value: 'created_06_build'),
                                text(name: 'OUTPUT_TEXT', value: 'created_06_build_content')
                            ]
                        )
                    }
                )
            }
        }
    }
}
