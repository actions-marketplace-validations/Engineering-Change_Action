# Engineering-Change/Action@v1.0.0

> Step one

Create your repository as you normally would, add a readme and license (as needed).

> Step two

Open a codespace or download and git clone the repo to initialize using command line as I
will guide you through the process from start to finish

> Step three

`git pull origin main`

`npm init -y`

`npm install @actions/core @actions/github`

`npm install -g @vercel/ncc`

`ncc build index.js -o dist`

`touch index.js`

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

`touch action.yml`
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
