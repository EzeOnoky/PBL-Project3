# PBL-Project3

# Implement Web solution based on MERN stack in AWS Cloud

In this project, i will implement a web solution based on MERN stack in AWS Cloud.

MERN Web stack consists of following components:
- **MongoDB** : A document-based, No-SQL database used to store application data in a form of documents.
  
- **ExpressJS** : A server side Web Application framework for Node.js.

- **ReactJS** : A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components

- **Node.js** : A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

![PBL3_Picture1](https://user-images.githubusercontent.com/122687798/219295295-2f4b71f3-bb5b-4651-aea2-313b81faa2c3.JPG)

As shown on the illustration above, a user interacts with the ReactJS UI components at the application front-end residing in the browser. This frontend is served by the application backend residing in a server, through ExpressJS running on top of NodeJS.

Any interaction that causes a data change request is sent to the NodeJS based Express server, which grabs data from the MongoDB database if required, and returns the data to the frontend of the application, which is then presented to the user.


# STEP 1 – BACKEND CONFIGURATION

## 1A  - INSTALL NODE.JS & NPM, CREATE PACKAGE.JSON

Firstly, We run the commands below: To update Ubuntu, upgrade Ubuntu

```
sudo apt update
sudo apt upgrade
```

Next, we get the location of the **Node.js** software from the ubuntu repository by running this command:

`curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

After doing the above, we can now install the **Node.js** and **npm** by running below command:


`sudo apt-get install -y nodejs`

The command above installs both *nodejs* and *npm*
NPM is a package manager for Node like apt for Ubuntu, it is used to install Node modules & packages and to manage dependency conflicts.

To check the version the node and check the version of the npm, we execute below...

```
node -v
npm -v
```

Next we create a directory for our To-Do Project, run the ***ls*** command to verify that the directory was created, and the CD into the ToDo directory

```
mkdir Todo
ls
cd Todo
```

Next, we initialize the project so that a new file **package.json** will be created. This file contains information of the application and the dependencies it nedds to run.

We initialize the project by running the command, We also run the ls command to verify that **package.json** was created.

**NOTE** The command npm init is used to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes.

```
npm init
ls
```
![3_1](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/a4156e75-44be-4377-b553-1fed5e397b7b)



Next we install ExpresJs and create the Routes directory.

## 1B   - INSTALL EXPRESSJS

Express is a framework for **Node.js**, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.

Express is a framework for **NodeJs**, Express helps to define routes of your application based on HTTP methods and URLs.

To use Express, we install it using npm:

`npm install express`

![3_2](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/4a5fbd1e-157e-468f-beb4-49d3260e7b38)


Now create a file **index.js**, and then run ***ls*** to confirm that the **index.js** file is successfully created. Next, install the dotenv module by running the command:

```
touch index.js
ls
npm install dotenv
```

Open the **index.js** file by running the command, We copy the folowing into it and "save" using ":wq"

`vim index.js`

```
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```

We start our server to see if it works. Before we start the server, we need to be sure we are in the Todo directory.

`node index.js`

If there are no erros, we should see ***Server running on port 5000*** in your terminal.

We need to go to our instance security group and edit inbound rules and add rules

We open our browser and put in the URL

http://<PublicIP>:5000

We should see ***welcome to Express***

![3_5](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/f5f0a0ff-313d-45cb-b56c-c6aa55d4d837)

Our To-Do application should be able to do the following:

- create a new task.
- dislay the lists of tasks.
- Delete a completed task
  
We need to create routes that will define various endpoints that the To-do application will depend on.

To create a folder routes, we run the command, Change into the routes directory, create a file **api.js**:

```
mkdir routes
cd routes
touch api.js
```

Open the file

`vim api.js`

We then copy and paste the code below into the **api.js** file

```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```

"save" and "quit" using ":wq"


## 1C  CREATING MODELS

We then go ahead to create **Models** since the application will be using **MongoDB** which is a NoSQL database. A Model makes the javascript application interactive. We also use Models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document.

The **Schema** shows how the database will be setup, including other data fields that may not be required to be stored in the database.

To create a Schema and a model, we will need to install **mongoose** which is a **Node.js** package that makes working with mongodb easier.

To install Mongoose, we make sure we are in the Todo directory then run the command:

`npm install mongoose`

![3_6](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/0d54e489-f094-406a-b273-6655d7cca42e)

We go ahead to create a folder **models** , then change into the model directory, Inside the models folder, create a file named **todo.js**

```
mkdir models
cd models
touch todo.js
```

![3_7](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/c8978b16-52c7-4e61-b2d3-34456beef397)

We then open the file and paste the following codes:

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;
```

![3_8](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/7988a3a6-6030-42b2-b670-3ed56343af00)

We then go to our routes directory and update the **api.js** file to be able to make use of the new model. Also Open the **api.js** file using the vim command

```
cd routes
vim api.js
```

Copy and paste the following codes into the file

```
const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;
```

![3_9](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/6a6b4dfd-0faa-481d-86d5-9bb63fa92eea)

Next we setup the MongoDB Database.

## 1D    SETTING UP THE MONGODB DATABASE

We use **MongoDB Database** to store our data using **mLab** which provides Database as a service (DBaas) solution.

To continue, we sign up [here](https://www.mongodb.com/atlas-signup-from-mlab).

Follow the sign up process, select AWS as the cloud provider, and choose a region near you.


![3_10](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/addf6b40-8e5b-496c-a62f-0ea6d6c96d08)

Go to **Network access**, select **Allow access from anywhere**. This is not secure but good for testing purposes.

![3_11](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/d0b0d7e4-bba2-45f0-900f-91bc3511e1b4)

Then change the time of deleting the entry from 6 Hours to 1 Week.


![3_12](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/a3fcac09-b602-4aae-b909-d4022f1306c8)

Create a **MongoDB** database and collection inside mLab by clicking on **"database"**, click on **cluster0** and then open **collections**.

![3_13](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/4b970ca3-d71d-476a-a92c-a62a18e112f6)

In the **index.js** file, we specified **process.env** to access environment variables, but we are yet to create this file.

To create the **process.env** file, we create a file in Todo directory and name it **.env** , Open the file

```
touch .env
vim .env
```

Add the connection string to access the database in it, just as below:

`DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'`

Make sure to update **"<username, <password, <network-address"** and **<database** according to your setup.

To get the connection string, we click on **"cluster0"** then click on **"connect"**

![3_14](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/f3d7550b-9cc4-4c5f-9386-54b999bd2b55)

Then we click on **"Mongodb drivers-connect your application..."**


![3_15](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/dbeb9014-24a7-4dc4-93e6-bd53b7238c70)

We then copy then connection string displayed into the **.env** file.

![3_16](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/0e374f54-df20-4e8b-9f29-c35fc69b72ed)

![3_17](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/af669d7d-12b9-45c8-be85-b74c2407b488)

We need to update the **index.js** to reflect the use of **.env** so that **Node.js** can connect to the database.

To do that we open the **index.js** file and delete the content using "esc" then ":%d" then "enter".

We then replace then content with the following codes:

```
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```

![3_18](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/7dc47bc7-cbd1-48d1-a708-46ae1c569ef1)

It is more secure to use environment variables to store information so as to separate configuration and secret data from the application, instead of writing connection strings directly inside the **index.js** application file.

We start our server by running the command:

`node index.js`

If the setup has no errors, we should see **"Database connected successfully"**

![3_19](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/a5d2f579-97c1-4b08-a586-a0ffb3eeec66)

We now have our backend configured, but we need to test it.

To test the backend without the frontend we are going to be using **Restful API** with the help of an API development client **Postman**

To download and install Postman, click [here](https://www.postman.com/downloads/) .

Click [here](https://www.youtube.com/watch?v=FjgYtQK_zLE) to learn how to perform [CRUD Operations](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) on Postman.

We test all the API endpoints and make sure they are working. For the endpoints that require body, you should send **JSON** back with the necessary fields since it’s what we setup in our code.

Now open your Postman, create a POST request to the API

`http://<PublicIP>:5000/api/todos`

This request sends a new task to our To-Do list so the application could store it in the database.

Make sure to set the header **"content-type"** and **"application/json"** :

![3_20](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/603bd328-f870-4e66-9fbc-f823f523521f)

Then click on **body.** In the field below we key in a command that displays as a response on then next field with an **id.**

![3_21](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/774ffd6f-729d-41f7-9c38-4bbdf29e1966)

Create a **GET** request to your API on

`http://<PublicIP>:5000/api/todos`

This request retrieves all existing records from out To-do application. The backend requests these records from the database and sends it us back as a response to **GET** request.

![3_22](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/a192b777-bf44-44b3-a2f4-4d68cdc33457)

To delete a task – you need to send its ID as a part of **DELETE** request.

By now you have tested backend part of our To-Do application and have made sure that it supports all three operations we wanted:

- Display a list of tasks – HTTP GET request
- Add a new task to the list – HTTP POST request
- Delete an existing task from the list – HTTP DELETE request

**We have successfully created our Backend, now let go create the Frontend.**

# STEP 2 – SETTING UP THE FRONTEND

We will create a user interface for a Web client (browser) to interact with the application via API.

To do this, we will start by running the command in the **Todo** directory:

`npx create-react-app client`

This will create a new folder in your Todo directory called client, where you will add all the react code.

![3_23](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/6d5bf069-aa00-43d3-b42d-c1e25a9cdf6d)


## 2A    RUNNING A REACT APPLICATION

There are some dependencies that need to be installed before running the **React App**

We Install "concurrently" by running the command:

`npm install concurrently --save-dev`

It is used to run more than one command simultaneously from the same terminal window.

![3_24](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/32f631a4-3c54-4534-a0a8-a7a1ed8994e7)

Next, we install **"nodemon"**. This is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.

`npm install nodemon --save-dev`

![3_25](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/ea271ca6-8fbd-4a7d-9e29-666069828b34)

Goto the Todo directory, open the **package.json** file.

`vim package.json`

In this file, replace the **"scripts"** section with the following code:

```
"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},
```

![3_26](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/f1e1e57a-5bb5-4dfa-9770-3578f8120838)

Change into the client directory, Open **package.json** file, Add the key value pair in the package.json file

```
cd client
vim apckage.json
"proxy": "http://localhost:5000"
```

![3_27](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/009f5bb0-60fb-4127-94fc-ba169e0dfd00)

The aim of adding the proxy to the file is to make it possible to access the application directly from the browser by simply calling the server url like **http://localhost:5000** rather than always including the entire path like **http://localhost:5000/api/todos**

We go back to the Todo directory, Then run the command:

```
cd ..
npm run dev
```

The app should open and start running on **localhost:3000**

In order to be able to access the application from the Internet you have to open **TCP port 3000** on EC2 by adding a new Security Group rule. The same way the security group for TCP port 5000 was created. This is done by clicking edit inbound rules.


## 2B  CREATING YOUR REACT COMPONENTS

One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. Our **Todo** app will have two stateful components and one stateless component.

Go to Todo directory, Change into the src directory, Inside your src folder create another folder called **components**, Move into the components directory, Inside components directory create three files **Input.js, ListTodo.js** and **Todo.js** ....Open Input.js file

```
cd client
cd src
mkdir components
cd components
touch Input.js ListTodo.js Todo.js
vim Input.js
```

Copy and paste the following:

```
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
```

![3_28](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/92f7f314-ea37-4379-8fc2-afb31e0b68ed)









































## STEP 2   Installing the NodeSource Node.js 18.x repo...


## Populating apt-get cache...

+ apt-get update
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu jammy-security InRelease
Reading package lists... Done

## Confirming "jammy" is supported...

+ curl -sLf -o /dev/null 'https://deb.nodesource.com/node_18.x/dists/jammy/Release'

## Adding the NodeSource signing key to your keyring...

+ curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | tee /usr/share/keyrings/nodesource.gpg >/dev/null

## Creating apt sources list file for the NodeSource Node.js 18.x repo...

+ echo 'deb [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_18.x jammy main' > /etc/apt/sources.list.d/nodesource.list
+ echo 'deb-src [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_18.x jammy main' >> /etc/apt/sources.list.d/nodesource.list

## Running `apt-get update` for you...

+ apt-get update
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy InRelease
Hit:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-updates InRelease
Hit:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu jammy-backports InRelease
Hit:4 http://security.ubuntu.com/ubuntu jammy-security InRelease
Get:5 https://deb.nodesource.com/node_18.x jammy InRelease [4563 B]
Get:6 https://deb.nodesource.com/node_18.x jammy/main amd64 Packages [774 B]
Fetched 5337 B in 1s (5310 B/s)
Reading package lists... Done

## Run `sudo apt-get install -y nodejs` to install Node.js 18.x and npm
## You may also need development tools to build native addons:
     sudo apt-get install gcc g++ make
## To install the Yarn package manager, run:
     curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | sudo tee /usr/share/keyrings/yarnkey.gpg >/dev/null
     echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
     sudo apt-get update && sudo apt-get install yarn


ubuntu@ip-172-31-51-131:~$ sudo apt-get install -y nodejs
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following NEW packages will be installed:
  nodejs
0 upgraded, 1 newly installed, 0 to remove and 1 not upgraded.
Need to get 28.5 MB of archives.
After this operation, 186 MB of additional disk space will be used.
Get:1 https://deb.nodesource.com/node_18.x jammy/main amd64 nodejs amd64 18.14.0-deb-1nodesource1 [28.5 MB]
Fetched 28.5 MB in 0s (70.3 MB/s)
Selecting previously unselected package nodejs.
(Reading database ... 92360 files and directories currently installed.)
Preparing to unpack .../nodejs_18.14.0-deb-1nodesource1_amd64.deb ...
Unpacking nodejs (18.14.0-deb-1nodesource1) ...
Setting up nodejs (18.14.0-deb-1nodesource1) ...
Processing triggers for man-db (2.10.2-1) ...
Scanning processes...
Scanning linux images...

No services need to be restarted.
No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
ubuntu@ip-172-31-51-131:~$ node -v
v18.14.0
ubuntu@ip-172-31-51-131:~$ npm -v
9.3.1
ubuntu@ip-172-31-51-131:~$ mkdir Todo
ubuntu@ip-172-31-51-131:~$ ls
Todo
ubuntu@ip-172-31-51-131:~$ cd Todo
ubuntu@ip-172-31-51-131:~/Todo$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (todo)
version: (1.0.0)
description: A todo app
entry point: (index.js)
test command:
git repository:
keywords: todo application
author: Eze Onoky
license: (ISC)
About to write to /home/ubuntu/Todo/package.json:

{
  "name": "todo",
  "version": "1.0.0",
  "description": "A todo app",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "todo",
    "application"
  ],
  "author": "Eze Onoky",
  "license": "ISC"
}


Is this OK? (yes) yes
npm notice
npm notice New minor version of npm available! 9.3.1 -> 9.5.0
npm notice Changelog: https://github.com/npm/cli/releases/tag/v9.5.0
npm notice Run npm install -g npm@9.5.0 to update!
npm notice
ubuntu@ip-172-31-51-131:~/Todo$ ls
package.json
ubuntu@ip-172-31-51-131:~/Todo$

## INSTALL EXPRESSJS

Remember that Express is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.


ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000
ubuntu@ip-172-31-51-131:~/Todo$ mkdir routes
ubuntu@ip-172-31-51-131:~/Todo$ cd routes
ubuntu@ip-172-31-51-131:~/Todo/routes$ touch api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ vim api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ ubuntu@ip-172-31-51-131:~/Todo/routes$
ubuntu@ip-172-31-51-131:~/Todo/routes$

![PBL3_Picture2](https://user-images.githubusercontent.com/122687798/219301120-7c74adb6-144a-4567-a2c1-6a910670b2d7.JPG)

## MODELS

Now comes the interesting part, since the app is going to make use of Mongodb which is a NoSQL database, we need to create a model. A model is at the heart of JavaScript based applications, and it is what makes it interactive. We will also use models to define the database schema . This is important so that we will be able to define the fields stored in each Mongodb document.

In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database. These are known as virtual properties.To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier

ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000


mkdir routes
:qa
cd

sudo -i
curl -s http://169.254.169.254/latest/meta-data/public-ipv4
:q
q
exit
ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000

ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js

ubuntu@ip-172-31-51-131:~/Todo$ npm install express

added 57 packages, and audited 58 packages in 2s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ touch index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ npm install dotenv

added 1 package, and audited 59 packages in 463ms

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  node_modules  package-lock.json  package.json
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
Server running on port 5000^C
ubuntu@ip-172-31-51-131:~/Todo$ mkdir routes
ubuntu@ip-172-31-51-131:~/Todo$ cd routes
ubuntu@ip-172-31-51-131:~/Todo/routes$ touch api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ vim api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ ubuntu@ip-172-31-51-131:~/Todo/routes$
ubuntu@ip-172-31-51-131:~/Todo/routes$ npm install mongoose

added 102 packages, and audited 161 packages in 6s

12 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo/routes$ cd
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ npm install mongoose

up to date, audited 161 packages in 836ms

12 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
ubuntu@ip-172-31-51-131:~/Todo$ mkdir models
ubuntu@ip-172-31-51-131:~/Todo$ cd models
ubuntu@ip-172-31-51-131:~/Todo/models$ touch todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ ls
todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ vim todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ ubuntu@ip-172-31-51-131:~/Todo/models$
ubuntu@ip-172-31-51-131:~/Todo/models$
ubuntu@ip-172-31-51-131:~/Todo/models$ cat todo.js

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
//const TodoSchema = new Schema({
//action: {
//type: String,
//required: [true, 'The todo text field is required']
//}
//})
//
////create model for todo
//const Todo = mongoose.model('todo', TodoSchema);
//
//module.exports = Todo;
ubuntu@ip-172-31-51-131:~/Todo/models$ ls
todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ cd
ubuntu@ip-172-31-51-131:~$ ls
Todo
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  models  node_modules  package-lock.json  package.json  routes
ubuntu@ip-172-31-51-131:~/Todo$ cd routes/
ubuntu@ip-172-31-51-131:~/Todo/routes$ ls
api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ cat api.js

const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});


## MONGODB DATABASE

## Challenges Encountered
So there were alot of bugs on the script i ran earlier, attempts at server connection using node index.js command failed, util the bugs were removed. On Mongo DB, I was also unable to successfully connect from my windows terminal until i updated my current IP on the Mongo DB.

STEPS FOLLOWED...
We need a database where we will store our data. For this we will make use of mLab. mLab provides MongoDB database as a service solution (DBaaS), so to make life easy, you will need to sign up for a shared clusters free account, which is ideal for our use case.The signup process was followed.

PS C:\Users\EZEPC\Desktop\DevOps> ssh -i "PBL3_1.pem" ubuntu@ec2-54-160-80-149.compute-1.amazonaws.com
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-1030-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Fri Feb 17 02:12:27 UTC 2023

  System load:  0.0               Processes:             97
  Usage of /:   29.9% of 7.57GB   Users logged in:       1
  Memory usage: 21%               IPv4 address for eth0: 172.31.51.131
  Swap usage:   0%


 * Introducing Expanded Security Maintenance for Applications.
   Receive updates to over 25,000 software packages with your
   Ubuntu Pro subscription. Free for personal use.

     https://ubuntu.com/aws/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


Last login: Fri Feb 17 00:20:37 2023 from 105.112.182.126
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$
ubuntu@ip-172-31-51-131:~$ ls
Todo
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  models  node_modules  package-lock.json  package.json  routes
ubuntu@ip-172-31-51-131:~/Todo$ cat todo.js
cat: todo.js: No such file or directory
ubuntu@ip-172-31-51-131:~/Todo$ cd models/
ubuntu@ip-172-31-51-131:~/Todo/models$ ls
todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ cat todo.js

const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
//const TodoSchema = new Schema({
//action: {
//type: String,
//required: [true, 'The todo text field is required']
//}
//})
//
////create model for todo
//const Todo = mongoose.model('todo', TodoSchema);
//
//module.exports = Todo;
ubuntu@ip-172-31-51-131:~/Todo/models$ vim todo.js
ubuntu@ip-172-31-51-131:~/Todo/models$ cd
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ cd routes/
ubuntu@ip-172-31-51-131:~/Todo/routes$ ls
api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ vim api.js
ubuntu@ip-172-31-51-131:~/Todo/routes$ cd..

cd..: command not found
ubuntu@ip-172-31-51-131:~/Todo/routes$
ubuntu@ip-172-31-51-131:~/Todo/routes$ cd
ubuntu@ip-172-31-51-131:~$ cd Todo/
ubuntu@ip-172-31-51-131:~/Todo$ cat .env
DB = 'mongodb+srv://onokyeze:onoky@105.112.182.126/cluster0.o1a750v.mongodb.net?retryWrites=true&w=majority'
ubuntu@ip-172-31-51-131:~/Todo$ ls
index.js  models  node_modules  package-lock.json  package.json  routes
ubuntu@ip-172-31-51-131:~/Todo$ vim index.js
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
(node:1228) [MONGOOSE] DeprecationWarning: Mongoose: the `strictQuery` option will be switched back to `false` by default in Mongoose 7. Use `mongoose.set('strictQuery', false);` if you want to prepare for this change. Or use `mongoose.set('strictQuery', true);` to suppress this warning.
(Use `node --trace-deprecation ...` to show where the warning was created)
Server running on port 5000
Error: querySrv ENOTFOUND _mongodb._tcp.105.112.182.126
    at QueryReqWrap.onresolve [as oncomplete] (node:internal/dns/promises:251:17) {
  errno: undefined,
  code: 'ENOTFOUND',
  syscall: 'querySrv',
  hostname: '_mongodb._tcp.105.112.182.126'
}
^C
ubuntu@ip-172-31-51-131:~/Todo$ cat .env
DB = 'mongodb+srv://onokyeze:onoky@105.112.182.126/cluster0.o1a750v.mongodb.net?retryWrites=true&w=majority'
ubuntu@ip-172-31-51-131:~/Todo$ vim .env
ubuntu@ip-172-31-51-131:~/Todo$ vim .env
ubuntu@ip-172-31-51-131:~/Todo$ ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
(node:1243) [MONGOOSE] DeprecationWarning: Mongoose: the `strictQuery` option will be switched back to `false` by default in Mongoose 7. Use `mongoose.set('strictQuery', false);` if you want to prepare for this change. Or use `mongoose.set('strictQuery', true);` to suppress this warning.
(Use `node --trace-deprecation ...` to show where the warning was created)
Server running on port 5000
MongooseServerSelectionError: Could not connect to any servers in your MongoDB Atlas cluster. One common reason is that you're trying to access the database from an IP that isn't whitelisted. Make sure your current IP address is on your Atlas cluster's IP whitelist: https://docs.atlas.mongodb.com/security-whitelist/
    at Connection.openUri (/home/ubuntu/Todo/node_modules/mongoose/lib/connection.js:825:32)
    at /home/ubuntu/Todo/node_modules/mongoose/lib/index.js:411:10
    at /home/ubuntu/Todo/node_modules/mongoose/lib/helpers/promiseOrCallback.js:41:5
    at new Promise (<anonymous>)
    at promiseOrCallback (/home/ubuntu/Todo/node_modules/mongoose/lib/helpers/promiseOrCallback.js:40:10)
    at Mongoose._promiseOrCallback (/home/ubuntu/Todo/node_modules/mongoose/lib/index.js:1285:10)
    at Mongoose.connect (/home/ubuntu/Todo/node_modules/mongoose/lib/index.js:410:20)
    at Object.<anonymous> (/home/ubuntu/Todo/index.js:12:10)
    at Module._compile (node:internal/modules/cjs/loader:1226:14)
    at Module._extensions..js (node:internal/modules/cjs/loader:1280:10) {
  reason: TopologyDescription {
    type: 'ReplicaSetNoPrimary',
    servers: Map(3) {
      'ac-1ujm473-shard-00-01.o1a750v.mongodb.net:27017' => [ServerDescription],
      'ac-1ujm473-shard-00-02.o1a750v.mongodb.net:27017' => [ServerDescription],
      'ac-1ujm473-shard-00-00.o1a750v.mongodb.net:27017' => [ServerDescription]
    },
    stale: false,
    compatible: true,
    heartbeatFrequencyMS: 10000,
    localThresholdMS: 15,
    setName: 'atlas-1390n2-shard-0',
    maxElectionId: null,
    maxSetVersion: null,
    commonWireVersion: 0,
    logicalSessionTimeoutMinutes: null
  },
  code: undefined
}
^C
ubuntu@ip-172-31-51-131:~/Todo$ node index.js
(node:1257) [MONGOOSE] DeprecationWarning: Mongoose: the `strictQuery` option will be switched back to `false` by default in Mongoose 7. Use `mongoose.set('strictQuery', false);` if you want to prepare for this change. Or use `mongoose.set('strictQuery', true);` to suppress this warning.
(Use `node --trace-deprecation ...` to show where the warning was created)
Server running on port 5000
Database connected successfully

  
  ![PBL3_2](https://user-images.githubusercontent.com/122687798/219877009-0960814e-5535-4fe7-8bb9-6a305a28cd03.JPG)

  ![PBL3_3](https://user-images.githubusercontent.com/122687798/219877266-674b035a-5ace-4743-a023-f7356b199ea9.JPG)

  
Now that i see ‘Database connected successfully’, it means we have our backend configured. Now we are going to test it.  
 
## Testing Backend Code without Frontend using RESTful API  

## Chalenges encountered

  
So far we have written backend part of our To-Do application, and configured a database, but we do not have a frontend UI yet. We need ReactJS code to achieve that. But during development, we will need a way to test our code using RESTfulL API. Therefore, we will need to make use of some API development client to test our code.

In this project, we will use Postman to test our API. Postman has already been installed on the PC, now to test our API, we will perform CRUD operartions on Postman

CRUD operartions on Postman - CRUD means - Create, Rename, Update Delete any kind of resources using Postman  
  
It is advised to test all the API endpoints and make sure they are working. For the endpoints that require body, you should send JSON back with the necessary fields since it’s what we setup in our code.

Now open your Postman, create a POST request to the API http://<PublicIP-or-PublicDNS>:5000/api/todos. This request sends a new task to our To-Do list so the application could store it in the database.
  
## STEP 2 – FRONTEND CREATION
  
Since we are done with the functionality we want from our backend and API, it is time to create a user interface for a Web client (browser) to interact with the application via API. To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app. In the same root directory as your backend code, which is the Todo directory, run:
  
ubuntu@ip-172-31-63-190:~/Todo$ cat package.json
{
  "name": "todo",
  "version": "1.0.0",
  "description": "A todo app",
  "main": "index.js",
  "scripts": {
  "start": "node index.js",
  "start-watch": "nodemon index.js",
  "dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
  },
  "keywords": [
    "todo",
    "application"
  ],
  "author": "Eze Onoky",
  "license": "ISC",
  "dependencies": {
    "dotenv": "^16.0.3",
    "express": "^4.18.2",
    "mongoose": "^6.9.2"
  },
  "devDependencies": {
    "concurrently": "^7.6.0"
  }
ubuntu@ip-172-31-63-190:~/Todo$ vi package.json
ubuntu@ip-172-31-63-190:~/Todo$ vim package.json
ubuntu@ip-172-31-63-190:~/Todo$ cat package.json

{
  "name": "todo",
  "version": "1.0.0",
  "description": "A todo app",
  "main": "index.js",
  "scripts": {
  "start": "node index.js",
  "start-watch": "nodemon index.js",
  "dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
  },
  "keywords": [
    "todo",
    "application"
  ],
  "author": "Eze Onoky",
  "license": "ISC",
  "dependencies": {
    "dotenv": "^16.0.3",
    "express": "^4.18.2",
    "mongoose": "^6.9.2"
  },
  "devDependencies": {
    "concurrently": "^7.6.0"
  }
}
ubuntu@ip-172-31-63-190:~/Todo$ ls
client  index.js  models  node_modules  package-lock.json  package.json  routes
ubuntu@ip-172-31-63-190:~/Todo$ cd client/
ubuntu@ip-172-31-63-190:~/Todo/client$ ls
README.md  node_modules  package-lock.json  package.json  public  src
ubuntu@ip-172-31-63-190:~/Todo/client$ vim package.json
ubuntu@ip-172-31-63-190:~/Todo/client$ cat package.json
{
  "name": "client",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@testing-library/jest-dom": "^5.16.5",
    "@testing-library/react": "^13.4.0",
    "@testing-library/user-event": "^13.5.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "web-vitals": "^2.1.4"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
  "eslintConfig": {
    "extends": [
      "react-app",
      "react-app/jest"
    ]
  },
  "proxy": "http://localhost:5000",
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  }
}
ubuntu@ip-172-31-63-190:~/Todo/client$ cd ..
ubuntu@ip-172-31-63-190:~/Todo$ npm run dev

> todo@1.0.0 dev
> concurrently "npm run start-watch" "cd client && npm start"

[0]
[0] > todo@1.0.0 start-watch
[0] > nodemon index.js
[0]
[1]
[1] > client@0.1.0 start
[1] > react-scripts start
[1]
[0] sh: 1: nodemon: not found
[0] npm run start-watch exited with code 127
[1] (node:8300) [DEP_WEBPACK_DEV_SERVER_ON_AFTER_SETUP_MIDDLEWARE] DeprecationWarning: 'onAfterSetupMiddleware' option is deprecated. Please use the 'setupMiddlewares' option.
[1] (Use `node --trace-deprecation ...` to show where the warning was created)
[1] (node:8300) [DEP_WEBPACK_DEV_SERVER_ON_BEFORE_SETUP_MIDDLEWARE] DeprecationWarning: 'onBeforeSetupMiddleware' option is deprecated. Please use the 'setupMiddlewares' option.
[1] Starting the development server...
[1]
[1] Compiled successfully!
[1]
[1] You can now view client in the browser.
[1]
[1]   Local:            http://localhost:3000
[1]   On Your Network:  http://172.31.63.190:3000
[1]
[1] Note that the development build is not optimized.
[1] To create a production build, use npm run build.
[1]
[1] webpack compiled successfully

![PBL3_4](https://user-images.githubusercontent.com/122687798/219880051-0ca393b6-ae2b-45a3-acc0-7afd66e7a45c.JPG)
  
Your app should open and start running on localhost:3000

Important note: In order to be able to access the application from the Internet you have to open TCP port 3000 on EC2 by adding a new Security Group rule. You already know how to do it.
  
## Creating your React Components
One of the advantages of react is that it makes use of components, which are reusable and also makes code modular. For our Todo app, there will be two stateful components and one stateless component. From your Todo directory run...
cd client  

move to the src directory
cd src
  
Inside your src folder create another folder called components
mkdir components
Move into the components directory with
cd components
  
Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js.
touch Input.js ListTodo.js Todo.js

Open Input.js file
vi Input.js
Copy and paste the following  

import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
  
![PBL3_5](https://user-images.githubusercontent.com/122687798/219909746-6a736af4-8921-40c3-9897-96e3d57e2c89.JPG)
  
To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios
  
Move to the src folder
cd ..

Move to clients folder
cd ..

Install Axios
npm install axios
  
![PBL3_6](https://user-images.githubusercontent.com/122687798/219909839-e2e97efc-9770-4781-ade2-7c17234834be.JPG)

Sip a coffee, lets continue to our destination
  
## FRONTEND CREATION (CONTINUED) 

Go to ‘components’ directory
cd src/components

After that open your ListTodo.js
vi ListTodo.js

                    in the ListTodo.js copy and paste the following code

import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {

return (
<ul>
{
todos &&
todos.length > 0 ?
(
todos.map(todo => {
return (
<li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
)
})
)
:
(
<li>No todo(s) left</li>
)
}
</ul>
)
}

export default ListTodo
  
                      Then in your Todo.js file you write the following code

import React, {Component} from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {

state = {
todos: []
}

componentDidMount(){
this.getTodos();
}

getTodos = () => {
axios.get('/api/todos')
.then(res => {
if(res.data){
this.setState({
todos: res.data
})
}
})
.catch(err => console.log(err))
}

deleteTodo = (id) => {

    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if(res.data){
          this.getTodos()
        }
      })
      .catch(err => console.log(err))

}

render() {
let { todos } = this.state;

    return(
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos}/>
        <ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
      </div>
    )

}
}

export default Todo; 

                    We need to make little adjustment to our react code. Delete the logo and adjust our App.js to look like this.

                    Move to the src folder
cd ..

                    Make sure that you are in the src folder and run
vi App.js

                    Copy and paste the code below into it

import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
return (
<div className="App">
<Todo />
</div>
);
}

export default App;
After pasting, exit the editor.

In the src directory open the App.css

vi App.css
Then paste the following code into App.css:

.App {
text-align: center;
font-size: calc(10px + 2vmin);
width: 60%;
margin-left: auto;
margin-right: auto;
}

input {
height: 40px;
width: 50%;
border: none;
border-bottom: 2px #101113 solid;
background: none;
font-size: 1.5rem;
color: #787a80;
}

input:focus {
outline: none;
}

button {
width: 25%;
height: 45px;
border: none;
margin-left: 10px;
font-size: 25px;
background: #101113;
border-radius: 5px;
color: #787a80;
cursor: pointer;
}

button:focus {
outline: none;
}

ul {
list-style: none;
text-align: left;
padding: 15px;
background: #171a1f;
border-radius: 5px;
}

li {
padding: 15px;
font-size: 1.5rem;
margin-bottom: 15px;
background: #282c34;
border-radius: 5px;
overflow-wrap: break-word;
cursor: pointer;
}

@media only screen and (min-width: 300px) {
.App {
width: 80%;
}

input {
width: 100%
}

button {
width: 100%;
margin-top: 15px;
margin-left: 0;
}
}

@media only screen and (min-width: 640px) {
.App {
width: 60%;
}

input {
width: 50%;
}

button {
width: 30%;
margin-left: 10px;
margin-top: 0;
}
}
Exit

                                In the src directory open the index.css
vim index.css
  
                                 Copy and paste the code below:

body {
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
box-sizing: border-box;
background-color: #282c34;
color: #787a80;
}

code {
font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
monospace;
}

                                      Go to the Todo directory
cd ../..

                                      When you are in the Todo directory run:
npm run dev
  

Assuming no errors when saving all these files, our To-Do app should be ready and fully functional with the functionality discussed earlier: creating a task, deleting a task and viewing all your tasks.
  
  
  ![PBL3_7](https://user-images.githubusercontent.com/122687798/219917343-86cb9b60-a9a3-42f4-94af-14a6d2affb85.JPG)

  
  ![PBL3_8](https://user-images.githubusercontent.com/122687798/219917389-78f4f54f-f665-4cf1-8da2-fd8efdee8a26.JPG)

  
  ![PBL3_9](https://user-images.githubusercontent.com/122687798/219917419-60075565-d344-47df-af86-961c7d39425b.JPG)



## Challenges Encountered_Lessons learnt
Each projects i attempt upskills my proficiency in the use of Linux commands, i spent longer hours on the projects because of my zero experience in navigating Linux command. Thankfully the Engineers at Darey.io would always guide, but then the personal researches i did for myself online helped alot. I always try not to immediately run to the Engineers at Darey.io, i have come to understand that personnally troubleshooting why i got a different outcome...far from the expected outcome based on the project steps guide, has helped grow my confidence.

In this project i learnt how to edit a file using VIM command, i also learnt to always crosscheck your script, any missed letter will impact the expected outcome.

  
## Congratulations EZE
In this Project #3 I have created a simple To-Do and deployed it to MERN stack. I wrote a frontend application using React.js that communicates with a backend application written using Expressjs. I also created a Mongodb backend for storing tasks in a database. WE MOVE !!!
