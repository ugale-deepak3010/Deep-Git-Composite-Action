# Re-Usable Workflow

Below are steps

1. Create simple yml file here  
ugale-deepak3010/Deep-Git-Composite-Action/.github/workflows/BuildAndPublishDockerImg.yml  

code should be looks like this:

```
name: Build and Publish Docker Image
on:
  workflow_call:
    inputs:
      name: 
        required: true
        type: string
      script_path:
        required: true
        type: string
    secrets:
      password:
        required: true
jobs:
  build: 
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Greet the person
        run: echo "Hello---1--, ${{ inputs.name }}!"
        shell: bash

      - name: Install tree and display file tree
        run: |
          sudo apt-get update
          sudo apt-get install -y tree
          tree
        shell: bash

      - name: Run hello world script
        run: python ${{ inputs.script_path }}
        shell: bash

        
```

2. Then use this yml file from this location
ugale-deepak3010/DeepGitHubActions/.github/workflows/Consumer Workflow.yml
3. Code should be looks like below

```
name: Consumer Workflow

on:
  push:
    branches:
      - main

jobs:
  call_greeting:
 
    uses: ugale-deepak3010/Deep-Git-Composite-Action/.github/workflows/BuildAndPublishDockerImg.yml@main
    with:
      name: "De--2--epak"
      script_path: "./src/addition.py"
    secrets:
      password: "Pass123"
```
4. Use those git tag v1 commands to create tag and push
Commands:

```
git checkout main
git pull
git tag v1
git push origin v1
```

![image](https://github.com/user-attachments/assets/bda5cdc4-2a6e-4dd0-84a0-935cc472b907)

5. Once we done replace this line **@main** to **@v1**
`uses: ugale-deepak3010/Deep-Git-Composite-Action/.github/workflows/BuildAndPublishDockerImg.yml@v1`

**Note: main is branch name as well default tag name**
