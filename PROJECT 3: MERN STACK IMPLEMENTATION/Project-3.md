## This project requires implementing a web solution based on a MERN stack in the AWS Cloud.
### A __MERN__ Web stack consists of following components: <br/>

__* MongoDB:__ A document-based, No-SQL database used to store application data in a form of documents. <br/>
__* ExpressJS:__ A server side Web Application framework for Node.js. <br/>
__* ReactJS:__ A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components. <br/>
__* Node.js:__ A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser. <br/>

###### * This project has a prerequistie of creating an Ubuntu EC2 instance on my personal AWS account. That instance has a security policy attached which allows me to log into it using SSH on port22 from my local laptop. The creation and setup of this instance is not documented here. 
___
### <div align="center"> Step 1) – BACKEND CONFIGURATION </div>
* Step 1 (sub steps)
  * Upgrade Ubuntu
  * Install NPM and NodeJS
  * Create a directory and initialize our project application in it.
   
 __Run update to fetch the updated metadata on the packages.__
![Ubuntu update](./images/updateubuntu-3.PNG)

__Run Upgrade to get packages on the newest versions__
![Ubuntu upgrade](./images/ubuntuupgrade-4.PNG)

### Install Node.js on the server
__First,  I need to get the location of the Node.JS software from the Ubuntu repositories with the following command.__
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
![Locate node.js Software](./images/locatenodejs-4.PNG)

__Then install node.js__
```
sudo apt-get install -y nodejs
```

![AccesWeblocally](./images/installnodejs.PNG)

__Next step is to verify the installation of both NPM and nodejs. Then create a ToDo folder for my project application.__
![Verify & Create](./images/verifyandcreate.PNG)

__Run the NPM init command in order to initialize the project and create all the base needed components__
![Initialize Node.JS](./images/npminit.PNG)

__Check the contents fo the Package.json fole that was created by the init procedure__
![AccesWeblocally](./images/verifynodejs.PNG)
___
### <div align="center"> Step 2) – Install expressjs </div>
![AccesWeblocally](./images/installexpressandcreateindex-2.PNG)
![AccesWeblocally](./images/installdotenv.PNG)
![AccesWeblocally](./images/enterindexjscode.PNG)
![AccesWeblocally](./images/expressjsserverrunning.PNG)
![AccesWeblocally](./images/editinboundsecurityrules.PNG)
![AccesWeblocally](./images/connecttoexpress5000.PNG)
![AccesWeblocally](./images/createroutesfolderandapi.PNG)

![AccesWeblocally](./images/installmongoose.PNG)
![AccesWeblocally](./images/createmodelsdirandtodojs.PNG)
![AccesWeblocally](./images/updateroutesapi.PNG)
