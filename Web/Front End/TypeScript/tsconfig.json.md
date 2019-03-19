## 1. tsconfig.json

### 1.1 compilerOptions

1.1.1 **module: enum** 

``module``用於指定模塊的代碼生成規則，可以使用``commonjs``，``amd``，``umd``，``system``，``es6``，``es2015``，``none``這些選項。

選擇commonJS，會生成符合commonjs規範的文件，使用amd，會生成滿足amd規範的文件，使用system会生成使用ES6的system.import的代码。使用es6或者是es2015會產生包含ES6特性的代碼。

1.1.2 **target: enum**

``target``要complier成的js版本，可以使用``es3``, ``es5``, ``es2015``, ``es6``

1.1.3 **sourceMap: boolean**

``sourceMap``是當我們使用chrome dev tools時，當有錯誤是否我們能夠直接在js連回ts檔案格式去偵錯，通常只會在dev環境開啟（為方便偵錯），不然會讓產出的檔案變大

1.1.4 **noImplicitAny: boolean**

是否在型別設定為any時發出警告

1.1.5 **removeComments: boolean**

設置為true代表不輸出注解

1.1.6 **charset: string**

1.1.7 **declaration: boolean**

是否需要產生定義文件d.ts

1.1.8 **newLine: enum**

可以使用``CRLF``(預設)及``LF``

1.1.9 **noResolve: boolean**

設定為true時，不使用``///``引入模塊，需要以編譯的文件在列表中引入。

```javascript
/// <reference path="" />
import PI from './2A.ts';
```

1.1.10 **outFile: string(url)**

設定輸出文件，會合併多個ts文件

1.1.11 **outDir: string(url)**

輸出文件的根目錄

1.1.12 **pretty: boolean**

Prettier 錯誤訊息

1.1.13 **noImplicitUseStrict: boolean**

使不使用``use strict``

1.1.14 **rootDir: string(url)**

輸入文件的根目錄

1.1.15 **watch: boolean**

監視文件，若文件有異動，自動編譯

1.1.16 **emitDecoratorMetadata: boolean**


