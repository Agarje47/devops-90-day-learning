Q: what is YAML?
- YAML Stands for YAML aint markup language. its a human readable configuration data format commonly used to define CI/CD pipelines , application configuration , infrastructure settings and automation
- in devops yamal is particularly important because tolls such as github actions , kubernetes, ansible, docker compose, and many ci/cd platforms use yaml based configuration.
exm: 
    name: my first workflow

    on:
       push:
            branches:
               - main
    
jobs:
    build:
        runs-on:windows-latest

        steps:
            - name: checkout code
              uses: actions/checkout@v4

            - name: say hello
              run: echo "hello devops"

Q: where is a github actions YAML file stored?
- normally yaml files will saved inside the workflow folder which is stored in .github folder in any repo.
- exm: .github/workflows/day8-yaml.yml

Q: YAML syntax -- the most important rule
- YAML uses indentation to represent structure
- unlike JSON, YAML doesn't use {} and [] to defile every level.
exm:
    server:
        name: web-server
        environment: production

- the indentation tells yaml that name and environment belongs to server.
- avoid mixing tabs and spaces.

Q: what is string in yaml?
- text can written directly or we can use quotes "" as well
exm: name: devops  --- name : "devops"
- quotes become particularly useful when the value contains special characters or could otherwise be interpreted as another yaml data type

Q: numbers
- exm: 
     port: 443
     server_count: 3
     timeout: 30
- these are numeric values, in github actions however remember that when values are inserted into shell commands or environment variable , you may need to consider how the receiving command interprets them.

Q: boolean values
- YMAl supports boolean values such as:
    enabled: true
    debug: false
- this can represent a configuration switch.

Q: comments
- comments begin with #.
exm: # this is my devops workflow
        name: day 8 workflow
- comments are ignore by YAML parser.
- user comments to explain why something exists, not every obvious line.

Q: lists
- YAMl lists use -
exm:    servers:
            - web01
            - web02
            - web03
        
Q: nested structures
-exm:
    server:
        name: web01
        operating_system: windows
        environment:
            name: UAT
            region: ap-south-1
- notice the indentation name and operating_system belongs to server
 name and region under environment belongs to environment.

 Q:YAML vs JSON
 - YAML is generally easier for humans to read and write, this is why it is popular in devops configuration.
 exm: YAML
     server:
        name: web01
        port: 434
        enabled: true
    JSON
        {
            "server":{
                "name": "web01",
                "port": 443,
                "enabled": true
            }
        }

Q: name 
- define the workflow's name
exm:    name: application CI
- github displays this name in the actions section

Q: on
- defines when the workflow should execute.
exm:    on: 
          push:
            branches:
                - main
- this means run the workflow when code is pushed to the main branch.

Q: jobs
- defines the work that github actions needs to perform.
exm:    jobs:
            build:
- build is the job id

Q: runs-on
-specifies the runner where the job executes
exm:    runs-on: windows-latest

Q: steps
- a job contains steps
exm:     steps:
            - name: step 1
              run: echo "first step"

            - name: step 2
              run: echo "second step"
- this steps executes sequentially unless the workflow configuration introduces dependencies or other behavior.

Q: uses vs run
-run means execute the command like  in linux
    - name: show directory
      run: pwd
in windows 
    - name: show directory
      run: get-location
powershell
    - name: check services
      shell: powershell
      run: get-services
uses:
- uses is existing github action
        - name: checkout repository
          uses: actions/checkout@v4
means
        run--> execute a command /script
        uses--> use a existing action

Q: multiple commands
- use | when you need multiple lines
exm:    - name: system information
            run: |
                echo "starting"
                echo "checking system"
                echo "finished"
on windows powershell:
        - name: windows information
          shell: powershell
          run: |
             write-host "compute:"
             $env:COMPUTERNAME
             write-host "powershell:"
             $PSVersionTable.PSVersion
on linux:
        - name: linux information
          run: |
            echo "Hostname:"
            Hostname

            echo "user:"
            whoami

            echo "directory:"
            pwd


