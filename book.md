const pool = require('./pool');
const bcrypt =require ('bcrypt');
const Lost = require('./lost');
const Found =require ('./found');

function book(){

    find : function(book = null, callback){
        if(user){
            var field = Number.isInteger(book)?'id:'title';
    }
    let sql = 'SELECT * FROM Book_T WHERE ${field}=?';
    pool.query(sql,book,function(err,result){
        if(err) console.log(err);
        if(result.length){
            callback(result[0]);
        }else{
            callback(null);
        }
    });
},
    add : function(body,callback){
        let sql 'INSERT INTO Book_T VALUES(BookID=?,Title=?,Description=?,Picture=?,NumCopies=?);
        pool.query(sql,function(err;result){
            if(err)callback(null);
            else callback(result.insertId);
        });
},
    delete : function(id,callback){
        let sql ='DELETE FROM Book_T WHERE Title=? AND BookID=?';
        pool.query(sql,id,function(err,ret){
            if(err) console.log(err);
            callback();
        });
},
    list : function (callback){
        let sql = 'SELECT* Title FROM Book_T';
        pool.query(sql,function(err,ret){
            if(err) console.log(err);
            callback();
        });
},
}    
 module.exports = book;          