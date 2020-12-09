# evaluation-docs
Documentation and steps for evaluation

### Notes
It is possible to borrow a GitHub and npm user for the steps included in this process, or you can use your own. It will include pushing a component library to a new GitHub repository, and publishing the same component library to npmjs.

## Section 1. Component owner

### 1.0 Setting up the component library
1. Extract the contents from boilerplate.zip into an empty folder.
2. Change the name of the package in package.json to something else
3. Follow the package verification guide from https://github.com/dhis2designlab/scp-cli to configure your package for the platform. This includes defining the keyword, git repository, and the dhis2ComponentSearch property in package.json.
4. Run `npx -p "https://github.com/dhis2designlab/scp-cli#master" dhis2-scp-cli verify` to perform a local verification of your code. (Skipping eslint for now)
5. Run `npm run build` to build a production version of your libray.

### 1.1 Push your component library to GitHub
1. For your component library to be verified later on, it needs to be hosted in a public github repository. So go ahead and create a new public repository and push your component library.
   1. You can either use your own GitHub account or "borrow" a test acccount for this.
   2. `git init`
   3. `git add .`
   4. `git commit -m "Added base files"`
   5. `git remote add origin <GitHub url>`
   6. `git push --set-upstream origin master`
   
### 1.2 Publish your component library to npm
1. Run `npm login` and provide your username, password and email.
2. Run `npm publish` to publish your new package.

### 1.3 Apply for verification
1. First, you need to create a production tag in GitHub that matches your published npm package, i.e. version `v1.0.0`.
2. Fork https://github.com/dhis2designlab/scp-whitelist
3. Add your package identifier (name) and version to list.csv. This can also be done in the GitHub interface.
4. Create the pull request and let the pipeline run. A maintainer will look over the validation pipeline and approve it accordingly.

## Section 2. Maintainer

### 2.0 Check the pull request
1. Open the whitelist repo https://github.com/dhis2designlab/scp-whitelist
2. Open the pull request that was published earlier.
3. Check "Files changed" tab, and see that a package and version was added.
4. Go to the "Checks" tab, and check through the "Run cat - > event.json <<EOF" action.
5. Go through the action and pay attention to the "debug" and "info" console.logs
    1. Important to notice here is the different jobs it goes through. First, it clones the GitHub repo with the corresponding release tag and checks that the property in package.json are correct, and contain the necessary values. Checks for eslint and npm audit are skipped during the `pr-verify` command, and only run during the local `verify` command. 
    2. Check that the output ends with a "Verification passed" log to know that the steps have been passed.
6. Go back to the "Conversation" tab and merge the pull request. The package should now be marked in the website as verified.

## Section 3. Component consumer

### 3.0 Search for components
1. Open the website: https://dhis2designlab.github.io/scp-website/.
2. Test our the search and filters. E.g. use them to find a component you are interested in (or one that you just published in your component library.)
4. Identify the name, export, and keywords on the component card, and use it to navigate to the component's npm location.
