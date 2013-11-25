sequenty
========

An extremely simple synchronous sequential processing module for node

usage: 

<example 1>

var sequenty = require('sequenty'); 

function f1(cb) // cb: callback by sequenty
{ 
  console.log('I'm f1');
  cb(); // please call this after finshed
}

function f2(cb)
{
  console.log('I'm f2');
  cb();
}

sequenty.run([f1, f2]);

- result -

I'm f1
I'm f2

<example 2>

var f = [];
var queries = [ "select .. blah blah", "update blah blah"];

for (var i = 0; i < 2; i++)
{
  f[i] = function(cb, funcIndex) // sequenty gives you cb and funcIndex
  {
    db.query(queries[funcIndex]);
    cb(); // must be called
  }
}

sequenty.run(f);
