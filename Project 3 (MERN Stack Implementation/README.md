<h2> Project 3: MERN (MongoDB Express React NodeJS) Stack Implementation </h2>

<h4> Step 1 </h2>

Commands

* sudo apt update
* sudo apt upgrade
* curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
* sudo apt-get install -y nodejs
* node -v 
* npm -v 

  <img src = 'Node Installed.png'/>
  
* mkdir Todo
* ls
* cd Todo
* npm init

  <img src = 'Project Created.png'/>
 
* npm install express
* touch index.js
* npm install dotenv
* vim index.js

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

* node index.js

  <img src = 'NPM Website.png'/>
 
* http://ec2-34-207-112-87.compute-1.amazonaws.com:5000

  <img src = 'Welcome to Express.png'/>
  
* mkdir routes
* cd routes
* touch api.js
* vim api.js

      const express = require ('express');
      const router = express.Router();

      router.get('/todos', (req, res, next) => {

      });

      router.post('/todos', (req, res, next) => {

      });

      router.delete('/todos/:id', (req, res, next) => {

      })

      module.exports = router;
    
 * npm install mongoose
 * mkdir models
 * cd models
 * touch todo.js
 
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
    
* vim api.js
 
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
* touch .env
* vi .env

        DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'

* vim index.js

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

* node index.js

  <img src = 'Database Connected.png'/>

  Post Request

    <img src = 'Post Request.png'/>

  Get Request 

    <img src = 'Get Request.png'/>  

  Delete Request

    <img src = 'Delete Request.png'/>

<h4> Step 2: Frontend Creation </h4>

Commands
  
* npx create-react-app client
* npm install concurrently --save-dev
* npm install nodemon --save-dev
* cd client
* vi package.json
* npm run dev
* cd client
* cd src
* mkdir components
* cd components
* touch Input.js ListTodo.js Todo.js
* vi Input.js
* cd .., cd ..
* npm install axios
* cd src/components
* vi ListTodo.js
* vi Todo.js
* vi App.js
* vi App.css
* vim index.css
* cd ../..
* npm run dev

   <img src = 'Todo App.png'/>
  
