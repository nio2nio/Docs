## 1. tsconfig.json

### 1.1 compilerOptions

1.1.1 **module: enum** 
``module``用於指定模塊的代碼生成規則，可以使用``commonjs``，``amd``，``umd``，``system``，``es6``，``es2015``，``none``這些選項。
選擇commonJS，會生成符合commonjs規範的文件，使用amd，會生成滿足amd規範的文件，使用system会生成使用ES6的system.import的代码。使用es6或者是es2015會產生包含ES6特性的代碼。

1.1.2 **target: enum**
``target``要complier成的js版本，可以使用``es3``, ``es5``, ``es2015``, ``es6``
