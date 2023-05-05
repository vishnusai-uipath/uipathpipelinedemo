pipeline {
//     agent {
//       label 'uipath'
//   }
  agent any
  environment {
      MAJOR = '1'
      MINOR = '0'
  }
  stages {
      
    stage('Check Out')  {
        steps {
            git url: 'https://github.com/ppengkkang/uipathpipelinedemo.git', branch: 'main'
        }
    }
    
    stage ('InstallPlatform') {
      steps {
        UiPathInstallPlatform (
          traceLevel: "Verbose",
          //cliNupkgPath: "C:\\jenkinsagent\\workspace\\UiPath.CLI.Windows.23.2.8467.25277.nupkg",
          cliNupkgPath: "C:\\uipath\\nupkg\\UiPath.CLI.Windows.22.10.8438.32859.nupkg",
          //cliNupkgPath: "C:\\uipath\\jenkins\\workspace\\UiPath.CLI.Windows.23.2.8467.25277.nupkg",
          //cliVersion: "UiPath Windows CLI(ver.23.2.8467.25277)",
          //cliVersion: "WIN_23.2.8467.25277",
          cliVersion: "WIN_22.10.8438.32859",
          forceInstall: true
        )
      }
    }
    
    
    stage ('Pack') {
      steps {
        UiPathPack (
          outputPath: "Output\\${env.BUILD_NUMBER}",
          projectJsonPath: "project.json",
          version: [$class: 'ManualVersionEntry', version: "${MAJOR}.${MINOR}.${env.BUILD_NUMBER}"],
          useOrchestrator: true,
          traceLevel: "None",
          orchestratorAddress: "https://cloud.uipath.com/ppengkkang/DefaultTenant",
          orchestratorTenant: "DefaultTenant",
          credentials: [$class: 'UserPassAuthenticationEntry', credentialsId: 'ocadmin']
        )
      }
    }
  }
}

