# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)


## Set up an electron-react-project for native desktop applications
based on:
* [Getting Started with Electron by Creating a React App](https://www.section.io/engineering-education/desktop-application-with-react/)
* [samuelmeuli/action-electron-builder](https://github.com/samuelmeuli/action-electron-builder)

Follow these steps to set up a new electron-react-app-project:

### project setup
* run following commands
  ```bash
  npx create-react-app <desired-project-directory-name>
  cd <desired-project-directory-name>
  rm -rf .git
  npm i -D electron electron-is-dev
  npm i -D concurrently wait-on
  ```
* Open the project in your IDE
* Copy *public/electron.js* into your project
* copy package.json to your repository
  and modify names, descriptions, categories and so on to match your project
* copy the directory *resources* into your project
  and replace all Icons by new ones, suitable for your app
* Copy the directory *.github* into your project
* Copy the file *triggerRelease* into your project and make it executable
  
### Push the project to gitHub
* Go to gitHub and create a new repository (empty)
* Open a terminal and run following commands
  ```
  git init
  git add .
  git commit -m "initial commit"
  git remote add origin <repository-url>
  git branch -M main
  git push -u origin main
  ```
  
### setup snap
* Go to [your snaps](https://snapcraft.io/snaps) and register a nice snap name \
  The snap has to match the name defined in *package.json*
* Open a terminal and run following command
  ```bash
  snapcraft export-login --snaps <snap-name> -
  ```
  This will generate a macaroon token (base64-encoded). \
  Copy it
* Go to gitHub, to your repository
* Go to *Settings->Secrets->Actions*
* Click *New repository secret*
* Paste the copied base64-encoded token
* Give the token the name *snapcraft_token*

## Release/Build
Simply execute the *triggerRelease.sh* \
This will create an empty commit with message of the last commit, \
tag it with the version, defined in *package.json* \
and execute *git push && git push --tags*. \
This will trigger the gitHub action, to build the application binaries, \
push them to a new gitHub release and push the created snap file to snapcraft

## Important
* The version, defined in *package.json* have to match the semantic versioning naming conventions. \
  Examples of allowed versions:
  * 1.2.3
  * 4.5.6-alpha.7
  * 8.9.10-beta.11
  * 12.13.14-rc15
* Before you can release the same version again, you have to delete the gitHub release for this version
* The name, defined in *package.json* should never contain underscores, dashes or spaces