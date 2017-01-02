# Project structure

### Aliases

Every project should have alias for root repository in form of 'src/', so the source code files/modules/folders could be accessible by e.g.:
```javascript
const module = require('src/modules/module.js');
```
instead of:
```javascript
const module = require('../../../modules/module.js');
```
(where '../../..' is root project directory containing app source files)

### Naming files and folders

Files should be named in lower-case, e.g.:

* name.html
* module-name.js
* some-component-with-long-name.js
* components/
* some-component/
