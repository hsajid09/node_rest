# node_rest
crud project


const mysql= require('mysql');
const express= require('express');
const app= express();
// const bodyParser = require('body-parser');
// app.use(bodyParser.json);

const morgan= require('morgan');
app.use(morgan('combined'));

const mysqlconnection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: 'sony',
    database:'abc',
    insecureAuth : true 

});
mysqlconnection.connect((err) => {
    if(!err){
        console.log('db connected'); 
    } else {
        console.log('not connected...'+JSON.stringify(err, undefined, 2));
    }
    
});

app.get('/test', (req, res) =>{
    mysqlconnection.query('SELECT * FROM test where id=2', (err, rows, fields)=> {
        if(!err){
            console.log(rows);
            res.json(rows);
        }else {
            console.log('Failed');
        }

    });

});


app.get('/', (req, res) =>{
    console.log('Responding to root Route');
    res.send('Hello to ROOOT');

});


app.listen(3000, (req, res) =>{
    console.log('conected @ port#3000');

});
