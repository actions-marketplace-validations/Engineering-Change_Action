# Engineering-Change/Action@v1.0.0

<img src="https://github.com/Engineering-Change/Action/assets/31228460/0e944187-9ad5-4d3c-8156-29f113cd3f65" width="500">

## Overview

This guide walks you through the steps to create and deploy a GitHub action in your repository. 
>Follow the instructions below in order.

## Step 1: Create the Repository

Create your repository as you normally would. Add a `README.md` and a `LICENSE` file (if necessary).

## Step 2: Initialize Your Repository

Once your repository is created, you need to initialize it. Open a codespace or clone the repo to your local system, and then open a terminal window.

## Step 3: Set Up Your Action

Pull the latest changes from your repository and set up your node environment.

```bash
git pull origin main
npm init -y
npm install @actions/core @actions/github
npm install -g @vercel/ncc
```
## Now, create your action's main script and your action's metadata file:

`touch index.js`

`touch action.yml`

### Copy paste this to create default index.js

```javascript
const core = require('@actions/core');
const github = require('@actions/github');

try {
  // Get the input
  const nameToGreet = core.getInput('who-to-greet');
  
  console.log(`Hello ${nameToGreet}!`);
  
  const time = (new Date()).toTimeString();
  
  core.setOutput("time", time);
  
  // Get the JSON webhook payload for the event that triggered the workflow
  const payload = JSON.stringify(github.context.payload, undefined, 2);
  
  console.log(`The event payload: ${payload}`);
  
} catch (error) {
  core.setFailed(error.message);
}
```

### Copy paste this into your action.yaml file next

```yaml
name: 'YOUR NAME HERE'
description: 'YOUR DESCRIPTION HERE'
inputs:
  who-to-greet:
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  time:
    description: 'The time you greeted someone'
runs:
  using: 'node12'
  main: 'dist/index.js'
```

`mkdir -p .github/workflows`

`touch .github/workflows/test.yml` 

### Copy this into your test.yml file

```yaml
name: Test Workflow
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: (REPO-OWNER-HERE)/(REPO-NAME)@v1.0.0
    
    - name: Test action
      id: test
      uses: (REPO-OWNER-HERE)/(REPO-NAME)@v1.0.0
      with:
        who-to-greet: 'Mona the Octocat'

    - name: Get the output
      run: echo "The time was ${{ steps.test.outputs.time }}"
```

`git add .`

`git commit -m "Initial action setup"`

`git push origin main`

> create your tag

`git tag v1.0.0`

`git push origin v1.0.0`

> Step five

If done correctly when you go to your repo, you should be able to go to action section 
and see your own new GitHub action now running.
