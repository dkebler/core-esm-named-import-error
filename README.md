# Demonstrating that core esm support in V14 does not support a named import of a cjs dot export even though esm support via std/esm package does.

**the std/esm support can import cjs dot exports as named imports just fine but core esm v14 support cannot.**

This is a repo that allows recreating the issue with esm support of dot exports in cjs modules in V14 when using the `"type": "module"` key in package.json and how this is not an issue using esm support via std/esm.

# How

clone repo, install.

there are flavors of `package.json`, one with  `"type": "module"` for running core esm support in V14 and one without designed to be run with the [std/esm](https://github.com/standard-things/esm) package using the flag `-r esm`

## Runing using core esm support in V14

To use with esm support in V14 copy `esm-package.json` to `package.json`
do the same within the  `esm-module` package which is a folder in this repo

delete `/node_modules` and run `npm-install`

then `npm start`

you will get this error

```
file:///mnt/AllData/hacking/active-dev-repos/name-import-error/index.js:5
import { cjsDotExport as cjs } from 'example-cjs-module'
         ^^^^^^^^^^^^
SyntaxError: The requested module 'example-cjs-module' does not provide an export named 'cjsDotExport'

```
now comment out the lines in index.js
```
// import { cjsDotExport as cjs } from 'example-cjs-module'
// cjs()
```

run again `npm start` and you will see that the `esm-module` loads correctly using the `  "type": "module"` in it's `package.json`
and outputs  `Hello from esm module`

## Running using std/esm package

To see the cjs  module work as a named import with std/esm copy `std-esm-package.json` to `package.json` and the same in the `esm-module` folder/package

uncomment the lines in index.js
```
import { cjsDotExport as cjs } from 'example-cjs-module'
cjs()
```

delete `/node_modules` and run `npm-install`

then `npm start`

the output will be
```
Hello from esm module
Hello from cjs module
```

## Conclusion

**the std/esm support can import cjs dot exports as named imports just fine but core esm v14 support cannot.**
