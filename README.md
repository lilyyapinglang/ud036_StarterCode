# Launch the Apollo and NodeServer

Open a new command prompt and run below commands:

```
npm install
npm run build site_sample
npm run deploy

cd /nodeServer
npm install
npm run build
npm start
```

Then open http://localhost:5050/sampleapp/index.html


# PL SaaS Sample App

Sample App is an open source application, this is a simple starter app enables you to display some 3D model data in your browser. It is a browser based application and requires no installation at the local device. To get source code, please clone from [sample app repository](https://gitlab.industrysoftware.automation.siemens.com/pdfy2s/SampleApp) .

Sample App offers the following functionalities:   
1. General declarative UI framework 
2. Sign in and Authenticate
3. View 3D model(rotate,zoom in/out) 
4. Download stored 3D model to local device
5. Received and view notifications on user's operations on the models.

You can directly play with the Sample App via : https://viewer.vis.dev.sws.siemens.com/sampleapp/index.html  
Pre-requisite: Sign in is required in order to play with Sample App, therefore [sign up a developer account](../Tutorials/1SetupDevAccount.md) first.

Currently you cannot sign up an account by yourself. You need to fill an request form and apply account from SAM team. Details at http://civ6w178:3000/DevConsole


# Key functionality covered

Sample App offers the following functionalities:   
1. General declarative UI framework 
2. Sign in and Authenticate
3. View 3D model(rotate,zoom in/out) 
4. Download stored 3D model to local device
5. Received and view notifications on user's operations on the models.

It showcases the combined usage of a selection of PL PaaS MicroServices, including [Event Notification Service API](https://viewer.docs.sws.siemens.com/en/docs/PL20181210134853460/ens/html), [PLMvisWeb Viewer](https://gitlab.industrysoftware.automation.siemens.com/PLMVisWeb/PLMVisWeb/wikis/home) or , [Apollo Web App Framework](https://gitlab.industrysoftware.automation.siemens.com/Apollo/afx/wikis/home), [3D Visualization Service API](https://viewer.docs.sws.siemens.com/en/docs/PL20181210134853460/3dvis/html) , [Security and Access Management Service API](http://civ6w178:3000/services/sam/landing/landingPage.html), [Dataset Storage Service](http://civ6w178:3000/services/dss/landing/landingPage.html) in one web app.  

We cover each of them in the tutorial session.

# Run Locally
Sample App code is currently available on [gitlab](https://gitlab.industrysoftware.automation.siemens.com/pdfy2s/SampleApp) and can be used as a starter code to build your own App. For more details on pre-requisites, how to integrate PL PasS services and how to build, please go to Tutorials.

## Pre-requisites
1. [Visual Studio 2017](https://visualstudio.microsoft.com/vs/)/[Visual Studio Code](https://code.visualstudio.com/)  
2. [Nodejs](https://nodejs.org/en/)    

## Setup  
1. Clone this project or download it.
```
git clone https://gitlab.industrysoftware.automation.siemens.com/pdfy2s/SampleApp.git
```
2. Go to repository folder, then go to` ./src` folder.
4. Open a new command prompt under `./src` folder and run below commands:
```  
npm install
npm run build site_sample
npm run deploy

cd /nodeServer
npm install
npm run build
npm start
```

Then sample app will be up and running at http://localhost:5050/sampleapp/index.html   
(Depending on your network, it may take up to 5 minutes to fully load the page.)      
To sign in and play with the locally running app, you still need Siemens PL Developer access key and secret ([How to get one](../Tutorials/1SetupDevAccount.md))

To understand this sample, there are a couple of technologies as you may need to know for better understanding:  
- Use Node.js and Express.js to create the web framework
- Use npm to manage javascript package
- Use Gulp to automate tasks in your development workflow.
- Use PLMvisWeb Viewer to display 3D viewer in web browser.

# Sample App Architecture Diagram and Flow 

![Sample App Architecture diagram](../imgs/SampleApp Architect.png)

1. Sample App server uses NodeJS. Server retrieve UI content from [Apollo Web App Framework](https://gitlab.industrysoftware.automation.siemens.com/Apollo/afx/wikis/home).   
2. To authenticate, Sample App server call Authenticate with [Security and Access Management Service API](http://civ6w178:3000/services/sam/landing/landingPage.html).  
3. Once authenticated, you can load models, this is achieved by calling [Visualization Service](https://viewer.docs.sws.siemens.com/en/docs/PL20181210134853460/3dvis/html) Download Model API.   
4. Visualization Service Download API then call [Dataset Storage Service](http://civ6w178:3000/services/dss/landing/landingPage.html) API (where model data is stored) to cache model data.  
5. Fetched data will be cached, loaded and rendered by [PLMVisWeb (a Webgl-based viewer)](https://gitlab.industrysoftware.automation.siemens.com/PLMVisWeb/PLMVisWeb/wikis/home).  
6. Model load and download event will be listened and interacti with [Event Notifiction Service API](https://viewer.docs.sws.siemens.com/en/docs/PL20181210134853460/ens/html) to enable user to get notification alert.    

Note :Visualization Service is a backend service for translating JT/XT models into renderable data (BOD) and cache them in data storage services such as DSS/DDM. In order to render BOD in browser, you will need the 3D library which is maintained by PLMVisWeb team. We implement a loader in order to get BOD stream from Visualization Service and then pass the data into PLMVisWeb Toolkit in order to render the model.   


# Create your Developer Account 

Your Siemens Developer Account is your main identity.  To use any of PL PaaS Services, you will need an Developer Account.  

Go to Dev Console, follow the sign up process, you will get your developer account created. Once the account is created, the default user of this account would be admin user. The first(Admin) can then go into Dev Console to add additional users.  
Note ! : Currently we don't have dev console yet, account has to be requested created manually at  http://civ6w178:3000/DevConsole  

# Integrate authenticaton with your app
Once you have your Developer account, you can start to create your application. Once you set up an application, you will have a Client ID and Client Secret. You will need these in all other OAuth flows, and to complete every other tutorials.

However for now, to obtain Client ID and Client Secret that can be used to access PL Microservices APIs, you would have to register with Zeus Team which is in charge of SAM (Security and Access Management - an authentication service.) and get `ClientID` and `ClientSecret`, which can then be used to obtain API key. Fill an request form and apply account from SAM team. Details at http://civ6w178:3000/DevConsole

SAM Auth service authenticates and authorize your application using Webkey. As Webkey is official Identity provider for **all** applications. Applications need to integrated authentication via Webkey. SAM Auth service provides the ability to integrate Webkey authentication via Open Id Connect / OAuth 2.0 protocols.

Optionally, this service provides api to fetch API Keys for the logged in user. This allows the client application to make calls on behalf of the logged in user to services that accept an API key from SAM.  
![introsamauth](http://civ6w178:3000/services/samauth/landing/assets/images/introduction_sam_auth.png "Intro to SAM")

## Prerequisites

If you are not familiar with how OAuth works and how to integrate OAuth, it's helpful to refer to GitHub OAuth system.

**Basically here's a list of what you need**:  
**1. Client Id & Client Secret**  
You should register your app then the OAuth provider (Google, Facebook, GitHub, SAM, etc.) would give you a unique client Id and client Secret.

**2. Callback URL**  
Your web app should have a callback API to receive info from authorization server. SampleApp is using node.js server, this is handled by package `simple-oauth2`. Meanwhile the provider also needs to know this callback URL.

**3. Endpoints of OAuth provider**    
You should know the authorization endpoint of the OAuth provider.

## Authentication steps

Once you meet conditions above, here are 3 steps to follow to integrate authentication into your app.
1. To begin, obtain credentials for your client application.  

  NOTE: Currently registering your client application has to be done by sending an email to the Zeus team. A Self Administration Console Application will be provided in future to allow you to register and manage your client applications.  

  As part of registration the client application will have to provide the following information:

|Property	       |Required	    |Type	   | Value
| -------------  | :----------:| :-----------: |-----------: |
|AppName         |	Yes|	String|	An unique app name
|Redirect URI(s)|Yes - WebApps No - Desktop Apps	|String|	The redirect URIs are the endpoints to which the SAM Auth Server can send responses.|
|Post Logout URI(s)|	Optional|	String|	One or more url(s) to which SAMAuth should redirect when logout is complete|


Note: Your Client Application will be handling the Open Id Connect/OAuth 2.0 protocol at the specified callback URL. If there is a mismatch in URI the protocol will not be complete and the application will not receive the Access Key and Id Token.

Once the above information is provided to the Zeus team, you will be provided a client_id and client_secret via email.

2. Then your client application must request an access token from SAM Auth Server, extract the access keys from the response.  

 In SampleApp, this is achieved by : 

Add OAuth into services, in `\src\nodeServer\src\routes\myRouter.ts`:
```
    import * as simpleOauth2 from "simple-oauth2";
```

For more details and code samples on Authentication code flow, please refer to [SAM Authentication Code Flow](http://civ6w178:3000/services/samauth/developer_api_reference/authorization-code-flow.html)

3. Send those access keys on the request to the Siemens PLM Microservices API called by your application.Access Key is valid only for specific time and expires. Once expired you need to request new Access Key.  

Overall Sequence to Obtain Access Key
![Authentication Flow](../imgs/sam-auth-service-flow.png)

## Learn More

[Security and Access Management](http://civ6w178:3000/services/sam/landing/landingPage.html)

[AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers)

