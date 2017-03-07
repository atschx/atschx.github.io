---
layout: post
title:  Angular2 ongoing 
author: Albert
date:   2017-01-10 20:20:30
categories: tech
---

> 技术遍地开发，选择最适合自己和团队的，而不是techshow。

## TypeScript

### 1. npm 全局安装 [typescript](http://www.typescriptlang.org/) 

```sh
➜  ~ npm install -g typescript
/usr/local/bin/tsc -> /usr/local/lib/node_modules/typescript/bin/tsc
/usr/local/bin/tsserver -> /usr/local/lib/node_modules/typescript/bin/tsserver
/usr/local/lib
└── typescript@2.1.4
```

### 2. 安装 [Visual Studio Code](https://code.visualstudio.com/) 

环境基本初始化完成。

## 上手 Angular2

采用`angular-cli`构建项目原型:[hello-angular2](https://github.com/atschx/angular2-ongoing/tree/master/hello-angular2)

```sh
➜  angular2-ongoing git:(master) ng new hello-angular2
installing ng2
  create .editorconfig
  create README.md
  create src/app/app.component.css
  create src/app/app.component.html
  create src/app/app.component.spec.ts
  create src/app/app.component.ts
  create src/app/app.module.ts
  create src/assets/.gitkeep
  create src/environments/environment.prod.ts
  create src/environments/environment.ts
  create src/favicon.ico
  create src/index.html
  create src/main.ts
  create src/polyfills.ts
  create src/styles.css
  create src/test.ts
  create src/tsconfig.json
  create angular-cli.json
  create e2e/app.e2e-spec.ts
  create e2e/app.po.ts
  create e2e/tsconfig.json
  create .gitignore
  create karma.conf.js
  create package.json
  create protractor.conf.js
  create tslint.json
Directory is already under version control. Skipping initialization of git.
Installing packages for tooling via npm.
```

最后，cd hello-angular2

```sh
➜  hello-angular2 git:(master) ✗ npm start

> hello-angular2@0.0.0 start /Users/Albert/.repo/frontend/angular2-ongoing/hello-angular2
> ng serve

** NG Live Development Server is running on http://localhost:4200. **
Hash: 9453698d485250e32f58
Time: 8698ms
chunk    {0} main.bundle.js, main.bundle.map (main) 4.67 kB {2} [initial] [rendered]
chunk    {1} styles.bundle.css, styles.bundle.map, styles.bundle.map (styles) 1.77 kB {3} [initial] [rendered]
chunk    {2} vendor.bundle.js, vendor.bundle.map (vendor) 2.83 MB [initial] [rendered]
chunk    {3} inline.bundle.js, inline.bundle.map (inline) 0 bytes [entry] [rendered]
webpack: bundle is now VALID.
```

访问：http://localhost:4200

