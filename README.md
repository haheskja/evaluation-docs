# evaluation-docs
Documentation and steps for evaluation

## Section 1. Component owner

### 1.0 Setting up a workspace
1. Open up an empty folder
2. Run `npm init` and follow the steps to initialize an empty npm module
3. Install @dhis/cli-app-scripts with `npm install --dev @dhis2/cli-app-scripts` and react with `npm install react`
4. Copy the `src` folder from the boilerplate
5. Copy the `d2.config.js` file from the boilerplate
6. Add the following to package.json to specify where the build files will be located (will be generated from running `d2-app-scripts build`)
```
  "main": "build/cjs/lib.js",
  "module": "build/es/lib.js",
```
7. For your component library to be verified later on, it needs to be hosted in a public github repository. So go ahead and create a new public repository and push your component library.
   1. Use the testaccount
   2. `git init`
   3. `git add .`
   4. `git commit -m "Added base files"`
   5. `git remote add origin <>`
   6. `git push --set-upstream origin master`
8. Run `npm run build` to build a production version of your libray.
9.  You now have a working simple component library

Notes: Here it might instead be good to have created a simple project that can be cloned

### 1.1 Using scp-cli to verify your component library
1. Follow the package verification guide from https://github.com/dhis2designlab/scp-cli
2. Run `npx -p "https://github.com/dhis2designlab/scp-cli#master" dhis2-scp-cli verify` to perform a local verification of your code. (Skipping eslint for now)

### 1.2 Publish your component library to npm
1. Run `npm login` and provide your username, password and email.
2. Run `npm publish` to publish your new package.

### 1.3 Apply for verification
1. First, you need to create a production tag in GitHub that matches your published npm package, i.e. version `v1.0.0`.
2. Fork https://github.com/dhis2designlab/scp-whitelist
3. Add your package identifier (name) and version to list.csv. This can also be done in the GitHub interface.
4. Create the pull request and let the pipeline run. A maintainer will look over the validation pipeline and approve it accordingly.

## Section 2. Component consumer

### 2.0 Search for components
1. Open the website: https://dhis2designlab.github.io/scp-website/.
2. Find one of the components you created and published in your package (e.g. Sidebar).
3. Find a component related to covid for react.
