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

Due to [cross-platform issues related to case (in)sensitivity](http://stackoverflow.com/questions/1594014/how-do-i-explain-my-colleagues-that-filenames-should-not-contain-uppercase-chara/1594041#1594041).

### Naming branches

For fixes:

`fix/[task's number if specified-]short-fix-description`

For features:

`feature/[task's number if specified-]short-feature-description`
