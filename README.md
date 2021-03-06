# Filebaser
Filebaser is an engine for managing database documents like MongoDB.

### Installation
All dependencies of Filebaser are easily installed by npm.
```bash
    npm install
```

### Declaration
How to declare:
```javascript
    const FileBaser = require('filebase');

    fb = new FileBaser('databasefile.db');
```

### Querying
You can apply any filter like in MongoDB
```javascript
    let collection = fb.getColletion('users');

    let users = collection.find({
        limit: 10,
        where: {
            age: { gte: 18 }
            active: true
        }
    });
```

### Saving
For inserting and updating data we use a pattern similar to an ORM
```javascript
    let collection = fb.getCollection('users');

    let obj = {
        name: 'filebase',
        login: 'file.baser',
        pass: 'file@123baser#',
        age: 24,
        active: true
    };

    collection.save(obj);
```
After that this object received and unique ID for identification and was saved to memory.

##### Why saved on memory ?
Because we are talking about writing data into a file. Even NodeJS works asynchronously
it should sometime overload the app.
So to solve this problem we created a function called "flush()". It's reposible for
sending saved data directly to the database file.
E.g.: continuing from last example about inserting data.
```javascript
    collection.flush();
```

### Testing
For automated tests we're using Mocha. And, integrated with npm custom scripts, you can run that easily using
the following command.
```bash
    npm run test
```