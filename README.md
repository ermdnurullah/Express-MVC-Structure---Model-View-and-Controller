# Express MVC Structure - Model, View and Controller
```
express-mvc-structure
```
Express MVC Structure: As you know that express.js is a framework of Node.js. So, It makes easy to develop our web application. When you install express js using Express Generator tool, By default, It will not generate Controllers & Models folder. So, You have to create them yourself. Hence In this tutorial, I will learn you How to create a Model, View, and controller in Node.js Express.

How to Create Model, View, and Controller in Node.js Express

Before creating an MVC folder structure, you should know the following points.

MVC is the most popular & useful structure for web application and it describes as
Model - It can handle the database
View - It can handle the client-side web pages
Controller - It can control the request & response of Model & View

First of all, Install Express app using the Express Generator tool. If you don't know to install the express app, You can learn it through the following URL

How to Install Express Application Using Express Generator Tool 

After installing it, You will get the following basic folder structure of express.
myapp/
  |__bin/
  |__node_modules/
  |__public/
  |__routes/
  |__views/
  |__package-lock.json
  |__package.json
Create Model, View, and Controller in Express

Now you have to set up an installed express app in the proper MVC formate. Because It provides only views folder, So you have to create Controllers & Models folder into it.

Now, Follow the given Steps to create the MVC structure of Express.

myapp/
  |__bin/
  |__controllers/
  |     |__crud-controller.js
  |__models/
  |     |__crud-models.js
  |__node_modules/
  |__public/
  |__routes/
  |     |__crud-route.js
  |__views/
  |     |__crud-operation.ejs
  |__package-lock.json
  |__package.json


Express - Model

Model- In this folder, you can write the functionality & logics related to the Database like insert, fetch, update, delete queries. Even It takes the query request from the controller & sends the response back to the controller.

You can create a model in the myapp application through the following steps

Create a folder  models  in the the myapp application.
Create a file crud-model.js in the models. Even you can create more controller files.
Define some functionality in the crud-model.js as the following script

File Path- models/crud-model.js

File Name - crud-model.js

module.exports={

   
  createCrud:function(){
       data="Form data was inserted";
       return data;
  },
  fetchCrud:function(){
    data="data was fetched";
    return data;   
  },
  editCrud:function(editData){
    data= "Data is edited by id: "+editData;
    return data; 
  },
  UpdateCrud:function(updateId){
    data= "Data was updated by id: "+updateId;
    return data; 
  },
  deleteCrud:function(deleteId){
    data= "Data was deleted by id: "+deleteId;
    return data; 
  }
}




Include model file crud-model.js in the controller file crud-controller.js  of controllers using the following script.

var crudModel=require('../models/crud-model');
Express - View

View- In this folder, you can write HTML code for displaying a web page on the web browser. Even you can send the data from the controller to view for displaying data dynamically.

The view will be generated with the Basic Structure of Express App and It contains views folder

You can create web pages in the views folder  through the following steps
create a file crud-operation.ejs in the views folder.
write the HTML code as the following script. Even you can create another HTML file & write HTML code based on your project requirement.

File Name - crud-operation.ejs

<!DOCTYPE html>
<html>
  <head>
    <title>CRUD Operation</title>
    <link rel='stylesheet' href='/stylesheets/style.css' />
    <style>
        table, td, th {  
          border: 1px solid #ddd;
          text-align: left;}
        table {
          border-collapse: collapse;
          width: 50%;}
        .table-data{
          position: relative;
          left:150px;
          top:100px;}
        th, td {
          padding: 15px;}
        </style>
  </head>
  <body>
    <% if(typeof editData!='undefined'){ %>
        <h1><%= editData %></h1>
        <form method="POST" action="/crud/edit/<%=editId %>">
            <input type="submit" value="Update Data">
        </form>
        <% } else{ %>
            <h1>Crud Operation</h1>
            <h3>This is View Page</h3>
            <h4>Create Data</h4>
            <form method="POST" action="/crud/create">
                <input type="submit" value="Create Data">
            </form>
        <% } %>

        <br><br> <br><br>
        <table border="1" >
            <tr>
                <th><a href="/crud/form">Crud Form</a></th>
                <th><a href="/crud/fetch">Fetch Data</a></th>
                <th><a href="/crud/edit/5">Edit Data</a></th>
                <th><a href="/crud/delete/5">Delete Data</a></th>
            </tr>
            </table>
  </body>
</html>




You can load a view file crud-operation.ejs in the controller file crud-controller.js  of the controllers' folder using the following script.

 res.render('crud-operation');
Express - Controller

Controller- In this folder, you can write the functionality & logic to develop dynamic web applications. Even it takes the data request from the views & sends it to the model and sends the response back to the views.

You can create a model in the myapp application through the following steps

Create a folder  controllers  in the the myapp application.
Create a file crud-controller.js in the controllers. Even you can create more controller files.
Define some functionality in the crud-controller.js as the following script

Path - controllers/crud-controller.js

File Name - crud-controller.js

var crudModel=require('../models/crud-model');
module.exports={

 crudForm:function(req, res) {
    res.render('crud-operation');
},
createCrud:function(req,res){

    const createData=crudModel.createCrud();
    res.send('<h1>'+createData+'</h1>');

},
fetchCrud:function(req,res){
   
    const fetchData=crudModel.fetchCrud();
    res.send('<h1>'+fetchData+'</h1>');
    
},
editCrud:function(req,res){

    const editId=req.params.id;
    const editData= crudModel.editCrud(editId);
    res.render('crud-operation',{editData:editData,editId:editId});
},
UpdateCrud:function(req,res){

     const updateId=req.params.id;
     const updateData= crudModel.UpdateCrud(updateId);
     res.send('<h1>'+updateData+'</h1>');

},
deleteCrud:function(req,res){

    const deleteId=req.params.id;
    const deleteData= crudModel.deleteCrud(deleteId);
    res.send('<h1>'+deleteData+'</h1>');

}

}




Include model file crud-controller.js in the controller file crud-route.js  of Route folder using the following script.

var crudController=require('../controllers/crud-controller');
Express - Route

Route - In the route folder, you can create a custom route/link to execute the dynamic web pages.

The Route will be generated with the Basic Structure of Express App and It contains routes folder

You can create routes in the routes folder  through the following steps
Create a file crud-route.js in the routes folder.
Define some functionality in the crud-route.js as the following script

Path - routes/crud-route.js

File Name - crud-route.js

var express = require('express');
var crudController=require('../controllers/crud-controller');
var router = express.Router();

// curd form route
router.get('/form', crudController.crudForm );

// create data route
router.post('/create', crudController.createCrud);

// display data route
router.get('/fetch', crudController.fetchCrud);

// edit data route
router.get('/edit/:id', crudController.editCrud);

// update data route
router.post('/edit/:id', crudController.UpdateCrud);

// delete data route
router.get('/delete/:id', crudController.deleteCrud);

module.exports = router;




You have to load a route file crud-route.ejs in the root file app.js  of the myapp app using the following script.

var crudRouter = require('./routes/crud-route');
app.use('/crud', crudRouter);

Note-

Learn more about the route through the following official documentation

Read Route Documentation

Start the Node.js  server & run the following route
http://localhost:3000/crud/form




My Suggestion

Dear Developer, I hope you have learned how to create Model, View, Controller in Node.js Express. Now. So, you should continue to visit my website, I will share more Node.js & express.js tutorials for you.

If you have any questions & suggestions related to this article or web technology coding field, You should ask me through the below comment box.

Thanks for reading this tutorial…
