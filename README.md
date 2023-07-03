# Action

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

`touch action.yml`

`mkdir -p .github/workflows`

`touch .github/workflows/test.yml` 

`git add .`

`git commit -m "Initial action setup"`

`git push origin main`

> Step five

If done correctly when you go to your repo, you should be able to go to action section 
and see your own new GitHub action now running.
