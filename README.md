# parse-wrapper

## Introduction

This is a wrapper for Parse to simplifying codes for data retrieving and modifying from Parse.

Please be aware that this plugin is only meant to implement a minimal subset of features of Parse, that are sufficient to implement a simple application with Parse backend. Basically, only data retrieving and updating are supported. If you need more features of Parse, please use the [official SDK](https://www.npmjs.com/package/parse) instead.

## Syntax

### Initializing

#### Loading module

To load the plugin:
```
var parse = require('parse-wrapper');
```

#### .initialize(keyObject)

To initialize Parse with your own keys:
```

var keys = {
    appKey: 'fakeAppKey',
    jsKey: 'faleJSKey'
};
parse.initialize(keys);
```

### Retrieving data

#### .getAll(class, callback)

To get all objects belonging to class ```Test```:
```
parse.getAll('Test', function(err, data){
  console.log(data); // all the objects is printed out
});
```

#### .getSome(class, condition, callback)

To get all the objects matching some conditions (e.g. has attribute ```testing``` equal to ```true```) in class ```Test```:
```
parse.getSome('Test', {testing: true}, function(err, data){
  console.log(data);
});
```
The objects will be returned as an array.

#### .getOne(class, condition, callback)

This is similar to ```.getSome()```, but only the first match will be returned.
```
parse.getOne('Test', {testing: true}, function(err, data){
  console.log(data);
});
```

#### .getOneByID(class, id, callback)

To get the object with id of ```1234``` from class ```Test```:
```
parse.getOneByID('Test', '1234', function(err, data){
  console.log(data);
});
```

### Deleting data

#### .deleteOneByID(class, id, callback)

To delete the object with id of ```1234``` from class ```Test```:
```
parse.deleteOneByID('Test', '1234', function(err){
  if(!err)
    console.log('Object deleted!');
});
```

### Updating data

#### .updateOneByID(class, id, newObject, callback)

To replace the object with id of ```1234``` from class ```Test``` with object ```newObject```:
```
parse.updateOneByID('Test', '1234', newObject, function(err){
  if(!err)
    console.log('Object updated.');
});
```

### Counting Objects

#### .countSome(class, condition, callback)

This is similar to ```.getSome()```, but only the number of match(es) found will be returned.
```
parse.countSome('Test', {testing: true}, function(err, count){
  console.log('There are '+count+' matches.');
});
```

### Saving objects

### .save(class, obj. callback)

To save a new object ```obj``` into class `'Test'`:
```
parse.save('Test', obj, function(err, id){
  if(!err)
    console.log('Object successfully saved with id of '+id);
});
```