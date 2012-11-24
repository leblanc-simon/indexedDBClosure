indexedDBClosure
================

indexedDBClosure is a library to manipulate indexDB. View examples to see how to use.


How to use
==========

All tables save object. You will be able to search in the indexes of each table.

Initialize the database
-----------------------

Create a database with one table named todo.
The table "todo" will have :
* a key : id
* an index : name

```javascript
var database = new indexedDBClosure({
    name: 'indexedDBClosure-todo',
    version: 1,
    tables: [
        {name : 'todo', key : 'id', indexes : [{ name : 'name', key : 'name' }] }
    ]
});
```

Get an item by key
------------------

Retrieve an item by this key and log it

```javascript
database.ready(function(){
    database.get(['todo'], 1,
        function(item) {
            console.log(item);
        }
    );
});
```

Search item by index
--------------------

Search the term "my search" in the name field of todo table.
Log each item found and show the number item found.

```javascript
database.ready(function(){
    var count = 0;
    database.search(['todo'], 'name', 'my search',
        function(item) {
            count++;
            console.log(item);
        },
        function() {
            alert(count + ' items found');
        }
    );
});
```

Add an item
-----------

```javascript
database.ready(function(){
    var todo = {
        id: 1,
        name: 'My first todo'
    };
    database.add(['todo'], todo, function() {
        alert('This item is added');
    });
});
```

Remove an item
--------------

```javascript
database.ready(function(){
    database.remove(['todo'], 1, function() {
        alert('This item is removed');
    });
});
```

Update an item
--------------

```javascript
database.ready(function(){
    var todo = {
        id: 1,
        name: 'My first todo updated'
    };
    database.update(['todo'], 1, todo, function() {
        alert('This item is updated');
    });
});
```

Get all items
-------------

Get all items and for each execute a function

```javascript
database.ready(function(){
    database.getAll(['todo'], function(item) {
        console.log(item);
    });
});
```


License
=======

License BSD : http://opensource.org/licenses/bsd-license.php


Author
======

Simon Leblanc <contact@leblanc-simon.eu>