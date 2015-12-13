
prod-config
=========
configurations for multiple production environments

### Structure of Configuation Files
```

- conf
  * common.js
  * dev.js
  - test
    * common.js
    * test.js
    * test-ci.js
  - prod
    * common.js
    * prod-a.js
    * prod-b.js
    * prod-c.js
```

"-": directory

"*": file

### Content of Configuration File

conf/dev.js
```
module.exports = {
  production: false, // set NODE_ENV=development automatically
  db: {
    user: 'admin',
    passwd: 'admin',
  },
}
```

conf/prod/common
```
module.exports = {
  production: true, // set NODE_ENV=production automatically
  db: {
    user: 'admin',
    passwd: fs.readFileSync('/path/secret.js').db_passwd,
  },
}
```

### Deploy & Run

#### Development
```
export ENV=dev
node index.js
```

#### Production
```
export ENV=prod-a
node index.js
```

### Get Config
init config:
```
global.conf = require('prod-conf')
```

using config anywhere:
```
some_db.connect(conf.db, function() {
  console.log('database connected. user:', conf.db.user)
})
```
