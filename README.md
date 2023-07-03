# Engineering-Change/Action@v1.0.0

> Step one

Create your repository as you normally would, add a readme and license (as needed).

> Step two

Open a codespace or download and git clone the repo to initialize using command line as I
will guide you through the process from start to finish

> Step three

`npm init -y`

`npm install @actions/core @actions/github`

`npm install -g @vercel/ncc`

`ncc build index.js -o dist`

`touch index.js`

### copy paste this to create default index.js
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
### copy paste this into your yaml file next
```yaml
name: 'Hello World'
description: 'Greet someone and record the time'
inputs:
  who-to-greet:  # id of the input
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

`git add .`

`git commit -m "Initial action setup"`

`git push origin main`

> Step five

If done correctly when you go to your repo, you should be able to go to action section 
and see your own new GitHub action now running.
