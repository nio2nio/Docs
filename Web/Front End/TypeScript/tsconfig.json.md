## 1. tsconfig.json

### 1.1 compilerOptions

1.1.1 **alwaysStrict: boolean**

Parse in strict mode and emit ``use strict`` for each source file.

1.1.2 **baseUrl: string**

Base directory to resolve non-relative module names.

1.1.3 **charset: string**

The character set (Default: ``UTF8``) of the input files.

1.1.4 **declaration: boolean**

Generates corresponding .d.ts file.

1.1.5 **module: enum**

Specify module code generation: ``None``, ``CommonJS``, ``AMD``, ``System``, ``UMD``, ``ES6``, ``ES2015`` or ``ESNext``.

1.1.6 **moduleResolution: enum**

Determine how modules get resolved. Either ``Node`` for Node.js/io.js style resolution, or ``Classic``.

1.1.7 **newLine: enum**

Use the specified end of line sequence to be used when emitting files: ``crlf`` (windows) or ``lf`` (unix).”.

1.1.8 **noImplicitAny: boolean**

Raise error on expressions and declarations with an implied any type.

1.1.9 **noImplicitUseStrict: boolean**

Do not emit ``use strict`` directives in module output.

1.1.10 **outDir: string**

Redirect output structure to the directory.

1.1.11 **outFile: string**

Concatenate and emit output to single file.

1.1.12 **pretty: boolean**

Stylize errors and messages using color and context.

1.1.13 **removeComments: boolean**

Remove all comments except copy-right header comments beginning with ``/*!``.

1.1.14 **rootDir: string**

Specifies the root directory of input files.

1.1.15 **sourceMap: boolean**

Generates corresponding .map file.

1.1.16 **target: enum**

Specify ECMAScript target version: ``ES3`` (default), ``ES5``, ``ES6/ES2015``, ``ES2016``, ``ES2017`` or ``ESNext`` (latest supported ES proposed features). 

1.1.17 **watch: boolean**

Run the compiler in watch mode. Watch input files and trigger recompilation on changes.

### 1.2 ``files`` property

```javascript
{
    "compilerOptions": {
        "module": "commonjs",
        "noImplicitAny": true,
        "removeComments": true,
        "preserveConstEnums": true,
        "sourceMap": true
    },
    "files": [
        "core.ts",
        "sys.ts",
        "types.ts",
        "scanner.ts",
        "parser.ts",
        "utilities.ts",
        "binder.ts",
        "checker.ts",
        "emitter.ts",
        "program.ts",
        "commandLineParser.ts",
        "tsc.ts",
        "diagnosticInformationMap.generated.ts"
    ]
}
```

### 1.3 ``include`` and ``exclude`` property

```javascript
{
    "compilerOptions": {
        "module": "system",
        "noImplicitAny": true,
        "removeComments": true,
        "preserveConstEnums": true,
        "outFile": "../../built/local/tsc.js",
        "sourceMap": true
    },
    "include": [
        "src/**/*"
    ],
    "exclude": [
        "node_modules",
        "**/*.spec.ts"
    ]
}
```

### 1.4 ``extends`` property

config/base.json
```javascript
{
  "compilerOptions": {
    "noImplicitAny": true,
    "strictNullChecks": true
  }
}
```

tsconfig.json
```javascript
{
  "extends": "./configs/base",
  "files": [
    "main.ts",
    "supplemental.ts"
  ]
}
```

### 1.5 ``compileOnSave`` property

```javascript
{
   "compileOnSave": true,
   "compilerOptions": {
       "noImplicitAny" : true
   }
}
```





