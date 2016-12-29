##Module README.md file schema:
```
#`Here goes module name`

`Here goes module description`

-
###Instalation
`npm i --save/--save-dev git://github.com/MariannaKrzewinska/some-repo.git#v1.0.27`

-
###Usage
`Here goes additional use information`
```
-
Every module if configurable should be initialized with config in form of js object in main application file (e.g. index.js, server.js etc).
```javascript
import * as moduleNameConfig from 'config/moduleNameConfig'; // or import { moduleNameConfig } from 'config'
import * as moduleName from 'moduleName';

moduleName.init(moduleNameConfig);
```
The structure of such configuration object should be described in 'Usage' section.
