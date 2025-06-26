pipeline {
    agent any  // Updated from 'label "UiPathLabel"' to run on any available agent

    environment {
        MAJOR = '1'
        MINOR = '0'
    }

    stages {

        stage('Check dotnet on the agent machine') {
            steps {
                script {
                    echo 'checking dotnet version...'
                    bat 'dotnet --version'
                    echo 'Printing PATH...'
                    bat 'echo %PATH%'
                    echo 'Displaying the location of the dotnet.exe...'
                    bat 'where dotnet'
                }
            }
        }

        stage('Build Package') {
            steps {
                echo "Start building the package on ${WORKSPACE}\\Output"
                UiPathPack(
                    credentials: ExternalApp(
                        accountForApp: 'techy_automation',
                        applicationId: '67b6e381-06f5-4745-9dd6-b11de69de887',
                        applicationScope: 'OR.Assets OR.BackgroundTasks OR.Execution OR.Folders OR.Jobs OR.Machines.Read OR.Monitoring OR.Robots.Read OR.Settings.Read OR.TestSetExecutions OR.TestSets OR.TestSetSchedules OR.Users.Read',
                        applicationSecret: 'UiPathSecretKey',
                        identityUrl: ''
                    ),
                    orchestratorAddress: 'https://cloud.uipath.com/',
                    orchestratorTenant: 'DefaultTenant',
                    outputPath: '${WORKSPACE}\\Output',
                    outputType: 'Process',
                    projectJsonPath: 'D:\\UiPath\\JenkinHellowordCloudIntegration\\project.json',
                    projectUrl: '',
                    repositoryBranch: '',
                    repositoryCommit: '',
                    repositoryType: '',
                    repositoryUrl: '',
                    splitOutput: false,
                    disableBuiltInNugetFeeds: false,
                    traceLevel: 'Verbose',
                    useOrchestrator: true,
                    version: CurrentVersion()
                )
            }
        }

        stage('Deploy Package') {
            steps {
                echo "Start deploying the package from ${WORKSPACE}\\Output"
                UiPathDeploy(
                    createProcess: true,
                    credentials: ExternalApp(
                        accountForApp: 'techy_automation',
                        applicationId: '67b6e381-06f5-4745-9dd6-b11de69de887',
                        applicationScope: 'OR.Assets OR.BackgroundTasks OR.Execution OR.Folders OR.Jobs OR.Machines.Read OR.Monitoring OR.Robots.Read OR.Settings.Read OR.TestSetExecutions OR.TestSets OR.TestSetSchedules OR.Users.Read',
                        applicationSecret: 'UiPathSecretKey',
                        identityUrl: ''
                    ),
                    entryPointPaths: 'Main.xaml',
                    environments: '',
                    folderName: 'Test',
                    ignoreLibraryDeployConflict: false,
                    orchestratorAddress: 'https://cloud.uipath.com/',
                    orchestratorTenant: 'DefaultTenant',
                    packagePath: '${WORKSPACE}\\Output',
                    processName: 'TestJenkinsDeployedPackage',
                    processNames: '',
                    traceLevel: 'Verbose'
                )
            }
        }

    }
}
