const pool = require('./pool');
const bcrypt =require ('bcrypt');
const Lost = require('./lost');
const Found =require ('./found');

function User(){

    find : function(user = null, callback){
        if(user){
            var field = Number.isInteger(user)?'id:'username';
    }
    let sql = 'SELECT * 
    FROM User_T 
    WHERE ${field}=?';
    pool.query(sql,user,function(err,result){
        if(err) console.log(err);
        if(result.length){
            callback(result[0]);
        }else{
            callback(null);
        }
    });
},
    signup : function(body,callback){
        var pwd =body.password;
        body.password = bcrypt.hashSync(pwd,10);
        var bind =;
        for(prop in body){bind.push(body[prop]);}
        
        let sql 'INSERT INTO USER_T(username,email,password,role)VALUES(?,?,?,0)';
        pool.query(sql,bind,function(err;result){
            if(err)callback(null);
            else callback(result.insertId);
        });
},
    signup_Admin : function(body,callback){
        var pwd =body.password;
        body.password = bcrypt.hashSync(pwd,10);
        var bind =;
        for(prop in body){bind.push(body[prop]);}
        
        let sql 'INSERT INTO USER_T(username,email,password,role)VALUES(?,?,?,1)';
        pool.query(sql,bind,function(err;result){
            if(err)callback(null);
            else callback(result.insertId);
        });
},
    login : function(username,password,callback){
        this.find(username,function(user){
            if(user){
                if(bcrypt.compareSync(password,user.password)){
                    callback(null);
                }
            }
        });
}
}    
 module.exports = User;          