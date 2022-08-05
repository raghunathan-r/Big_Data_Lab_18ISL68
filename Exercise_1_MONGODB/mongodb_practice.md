## Q1. Create a database cricket and make a collection with name teamindia and execute following quaries.

## 1.a. 
use cricket
db.createCollection("teamindia");

## 1.b.
db.teamindia.insert({ no: 1, name: "st", salary: 2000, role:"bat" });

db.teamindia.insertMany([
    
    {no: 2, name: "msd", salary: 1500, role:"wk" },
    {no: 3, name: "ys", salary: 1000, role:"alr" },
    {no: 4, name: "rd", salary: 1000, role:"bat" },
    {no: 5, name: "rs", salary: 500, role:"bat" },
    {no: 6, name: "bk", salary: 500, role:"bat" },
    {no: 7, name: "vk", salary: 300, role:"bwl" },
    {no: 8, name: "jb", salary: 400, role:"bwl" },
    {no: 9, name: "hp", salary: 400, role:"alr" },
    {no: 10, name: "vs", salary: 300, role:"bat" }
    
]);

## 1.c.
db.teamindia.find().pretty()

## 1.d.
db.teamindia.find({name: "vk"});
db.teamindia.updateMany({name: "vk"}, {$inc: {salary: 6000}});

## 1.e.
db.teamindia.find()
db.teamindia.updateMany({}, {$inc: {salary: 6000}})

## 1.f.
db.teamindia.find({name: "msd"})
db.teamindia.update({name: "msd"}, {$set: {role: "c and wk"}})

## 1.g.
db.teamindia.find({name: "rs"})
db.teamindia.update({name: "rs"}, {$set: {remark: "wc"}})

## 1.h.
db.teamindia.find({name: /^s/})

## 1.i.
## 1.j.
