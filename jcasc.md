Go to "Manage Jenkins"  ->  "Configuration as Code"

update yaml file with below code

```sh
jenkins:
  systemMessage: "AutomatingGuy demo: configured automatically with JCasC plugin\n\n"

  numExecutors: 3
  mode: NORMAL

tool:
  git:
    installations:
    - home: "git"
      name: "Default"

jobs:
  - script: >
        pipelineJob('demo_by_jcasc') {
          definition {
              cpsScm {
                  scriptPath 'Jenkinsfile'
                  scm {
                    git {
                        remote { url 'https://github.com/lewisice/api-test-demo.git' }
                        branch '*/cicd'
                        extensions {}
                    }
                  }
              }
          }
        }
```