## This project requires implementing a web solution based on a MERN stack in the AWS Cloud.
### A __MERN__ Web stack consists of following components: <br/>

__* MongoDB:__ A document-based, No-SQL database used to store application data in a form of documents. <br/>
__* ExpressJS:__ A server side Web Application framework for Node.js. <br/>
__* ReactJS:__ A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components. <br/>
__* Node.js:__ A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser. <br/>

###### * This project has a prerequistie of creating an Ubuntu EC2 instance on my personal AWS account. That instance has a security policy attached which allows me to log into it using SSH on port22 from my local laptop. The creation and setup of this instance is not documented here. 

## BACKEND CONFIGURATION

### Install the latest versions of all packages on the Ubuntu server.
   
 * __Run update to fetch the updated metadata on the packages.__ <br/>
 `sudo apt update`
![Ubuntu update](./images/updateubuntu-3.PNG)

* __Run Upgrade to get packages on the newest versions__ <br/>
`sudo apt upgrade`
![Ubuntu upgrade](./images/ubuntuupgrade-4.PNG)

### Install Node.js on the server and setup the application code
* __Locate the Node.js software on the Ubuntu repositories with the following command.__ <br/>
`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - `
![Locate nodejs Software](./images/locatenodejs-4.PNG)

* __Application code setup (install node.js)__ <br/>
_The following command  installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu_ <br/>
`sudo apt-get install -y nodejs`
![Install Nodejs](./images/installnodejs40.PNG)

* __Verify the installation of both NPM and nodejs. Then create a ToDo folder for my project application.__ <br/>
`node -v` <br/>
`npm -v` <br/>
`mkdir ToDo` <br/>
![Verify & Create](./images/verifyandcreate.PNG)

* __Initialize the project and create all the base needed components__ <br/>
`npm init`
![Initialize Node.JS](./images/npminit.PNG)

* __Verify the existence of the Package.json file that was created by the init procedure__ <br/>
`cat package.json`
![Verify Package Contents](./images/verifynodejs.PNG)

## INSTALL EXPRESSJS <br/>
* __Install expressjs and create an index.js file__ <br/>
*Expressjs is a framework layer built on the top of the Node js that helps manage servers and routes.* <br/>
`npm install express` <br/>
`touch index.js` <br/>
![Install Expressjs & Index](./images/installexpressandcreateindex-2.PNG)

* __Install the dotenv module__ <br/>
*DotEnv is a lightweight npm package that automatically loads environment variables from a .env file into the process.env object.* <br/>
![Install DotENV](./images/installdotenv.PNG)

* __Edit the index.js file with the following code__ <br/>
 *index.js is the "entry point" for my new nodejs application* <br/>
![Edit Index.js](./images/enterindexjscode.PNG)

* __Start the new nodejs applciaiton listening on TCP port 5000__ <br/>
![Startup Node.JS](./images/expressjsserverrunning.PNG)

* __Allow port 5000 on the security rules attached to the server instance which hosts my new application__ <br/>
![SecurityGroup Port5000](./images/editinboundsecurityrules.PNG)

* __Access the new application from a local web browser on port 5000__ <br/>
![Access app from Browser](./images/connecttoexpress5000.PNG)

* __Create the routes folder, also create and edit the api.js file in that new folder__ <br/>
*A route is a section of Express code that associates an HTTP verb (GET, POST, PUT, DELETE, etc.), a URL path/pattern, and a function that is called to handle that pattern.*
![Routes foler and AP](./images/createroutesfolderandapi.PNG)

## CREATING A MODEL <br/>
*A schema is fundamentally describing the data construct of a document.* <br/>
*A model is a compiled version of the schema. One instance of the model will map to one document in the database.*
* __Install Mongoose to provide functionality around creating and working with the schemas.__ <br/>
![Install Mnogoose](./images/installmongoose.PNG)

* __Create the models folder, also create and edit the ToDo.js file in that new folder__ <br/>
![Ceate Models folder](./images/createmodelsdirandtodojs.PNG)

* __Edit the api.js file in the routes folder as follows__ <br/>
*This code will be used to define the action taken when a sepcific endpoint is called.*
![Update routes API](./images/updateroutesapi-1.PNG)

## MONGODB DATABASE <br/>
*For my project I will need a database where I will store my data. For this I will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS).*

