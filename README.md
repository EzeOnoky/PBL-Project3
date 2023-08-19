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

To make use of **Axios**, which is a Promise based HTTP client for the browser and **node.js**

We go into the client directory and run the command:

```
cd ../..
npm install axios
```

We go to **components** directory:

`cd src/components`

After that we open the **ListTodo.js**

`vim ListTodo.js`

In the **ListTodo.js** copy and paste the following codes:

import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {

```
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
```

![3_29](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/0cb028ee-8a4a-496a-b7e9-6c1e3e4c1624)

Open the **Todo.js** file we copy and paste the following code:

```
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
```

We then move into the src directory, and Open **App.js** file.

```
cd ..
vim App.js
```

Copy and paste the following codes into the file

```
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
```

![3_30](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/8dd557f1-b3f2-4f76-863f-b7833a98ead5)

We Exit, Next we open the **App.css** file in the src directory and paste the following codes:

```
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
```

![3_31](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/58560193-b3bb-4b03-8aae-309fa284b7d2)

We Exit, still in the same src directory, we open the **index.css** file, and then copy and paste the following codes:

`vim index.css`

```
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
```

We go to the **Todo** directory, In the Todo directory, we then run the command - npm cmd

```
cd ../..
npm run dev
```

If there are no errors, there should be a message **webfiles compiled successfully**


![3_32](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/a4b97ee8-3d0c-46f9-a3d5-727ddbb009c6)

To view this on the browser, we past the URL:

http://<PublicIP>:3000

![3_33](https://github.com/EzeOnoky/Project-Base-Learning-3/assets/122687798/10cd7421-0678-46d0-a0ef-a8e71320be8e)

Our **To-do** application is ready and functional with the functionality discussed earlier: creating a task, deleting a task and viewing all your tasks.

# Congratulations Eze !
In this Project 3 you have created a simple To-Do and deployed it to **MERN** stack. You wrote a frontend application using **React.js** that communicates with a backend application written using **Expressjs**. You also created a **Mongodb** backend for storing tasks in a database.
