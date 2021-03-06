---
treee -L 1 -a -I node_modules --dirs-first

β­ important π very important

β‘ has read β³ to do π no need to read
---

#### `tree`

```
angular-cli
βββ .circleci
βββ .github
βββ .idea
βββ .yarn
βββ benchmark
βββ bin
βββ πdocs
βββ etcsalou
βββ integration
βββ lib
βββ πpackages
β   βββ angularπ
β   β   βββ cli
β   β   βββ pwa
β   βββ πangular_devkit
β   β   βββ πarchitectβ³
β   β   βββ architect_cliβ³
β   β   βββ benchmark
β   β   βββ β­build_angularβ³π
β   β   βββ build_ng_packagrβ‘
β   β   βββ ππbuild_optimizerβ³
β   β   βββ β­build_webpackβ³
β   β   βββ core
β   β   βββ β­schematics
β   β   βββ β­β­schematics_cli
β   βββ ngtools
β   β   βββ β­webpack
β   βββ β­schematics
β   β   βββ angularπ
β   β   βββ β­schematics
β   β   βββ updateπ
β   βββ _
β   β   βββ benchmark
β   β   βββ devkit
β   βββ README.md
βββ scripts
βββ tests
βββ third_party
βββ tools
βββ .bazelignore
βββ .bazelrc
βββ .bazelversion
βββ .editorconfig
βββ .gitattributes
βββ .gitignore
βββ .mailmap
βββ .monorepo.json
βββ .nvmrc
βββ .prettierignore
βββ .prettierrc
βββ .yarnrc
βββ BUILD.bazel
βββ CONTRIBUTING.md
βββ Dockerfile
βββ LICENSE
βββ package.json
βββ README.md
βββ renovate.json
βββ tsconfig-test.json
βββ tsconfig.json
βββ tslint.json
βββ WORKSPACE
βββ yarn.lock
```

#### docs

https://github.com/angular/angular-cli/blob/master/docs/design/build-system.md

docs/design/build-system.mdπ

https://angular-builders.dev/home

#### main

Angular CLI => Angular DevKit

@angular/compiler-cli

- ngc
- ngcc

  Angular Compatibility Compiler (ngcc)
  This compiler will convert node_modules compiled with ngc, into node_modules which appear to have been compiled with ngtsc.
  This conversion will allow such "legacy" packages to be used by the Ivy rendering engine.

```dot
digraph G {
  node [shape=rectangle];
  "assets array" -> "copy-webpack-plugin";
  "*.ts" -> "@ngtools/webpack" -> "@angular-devkit/build-optimizer";
  "*.js" -> "source-map-loader" -> "@angular-devkit/build-optimizer";
  "@angular-devkit/build-optimizer" -> "webpack module concatenation" -> "webpack bundling" -> "terser-webpack-plugin";
  "scripts array" -> "terser-webpack-plugin";
  "*.css" -> "postcss-loader with postcss-import, ./postcss-cli-resources.ts, autoprefixer";
  "*.scss\|sass" -> "sass-loader" -> "postcss-loader with postcss-import, ./postcss-cli-resources.ts, autoprefixer";
  "*.less" -> "less-loader" -> "postcss-loader with postcss-import, ./postcss-cli-resources.ts, autoprefixer";
  "*.styl" -> "stylus-loader" -> "postcss-loader with postcss-import, ./postcss-cli-resources.ts, autoprefixer";
  "postcss-loader with postcss-import, ./postcss-cli-resources.ts, autoprefixer" -> "raw-loader" [label="component style?"];
  "raw-loader" -> "./optimize-css-webpack-plugin.ts"
  "postcss-loader with postcss-import, ./postcss-cli-resources.ts, autoprefixer" -> "style-loader, ./raw-css-loader.ts, and mini-css-extract-plugin" [label="global style?"];
  "style-loader, ./raw-css-loader.ts, and mini-css-extract-plugin" -> "./optimize-css-webpack-plugin.ts"
}
```

##### html

angularjs εΊδΊζ΅θ§ε¨ζ§θ‘εζ΄ζ£ζ΅

the creation of the DOM was delegated to the browser, which parsed your HTML and created the DOM tree (thatβs its job, after all), and then AngularJS would run over the DOM elements, figure out the directives and text binding expressions and replace them with the actual data

ζ΅θ§ε¨δΈε DOM ζ δΈεοΌεΌεΈΈε€ηθ½εοΌθΏεΊ¦δΎθ΅ζ΅θ§ε¨οΌε€§ε°ει?ι’

angular ηΌθ―ε¨ε° html θ½¬ζ’ζ typescript

The compiler actually replaces the browser and parses the HTML for you.

![](https://miro.medium.com/max/1400/1*lY05KDubFcYpyc_QMAsyqg.png)

##### ngfactory

ngc

ngfactory

```bash
src
βββ app
β βββ route
β β βββ contacts
β β β βββ departments
β β β β βββ departments.component.css.shim.ngstyle.js
β β β β βββ departments.component.css.shim.ngstyle.js.map
β β β β βββ departments.component.js
β β β β βββ departments.component.js.map
β β β β βββ departments.component.metadata.json
β β β β βββ departments.component.ngfactory.js
β β β β βββ departments.component.ngfactory.js.map
β β β β βββ departments.component.ngsummary.json
β β β βββ list
β β β β βββ list.component.css.shim.ngstyle.js
β β β β βββ list.component.css.shim.ngstyle.js.map
β β β β βββ list.component.js
β β β β βββ list.component.js.map
β β β β βββ list.component.metadata.json
β β β β βββ list.component.ngfactory.js
β β β β βββ list.component.ngfactory.js.map
β β β β βββ list.component.ngsummary.json
β β β βββ contacts-common.service.js
β β β βββ contacts-common.service.js.map
β β β βββ contacts-common.service.metadata.json
β β β βββ contacts-common.service.ngfactory.js.map
β β β βββ contacts-common.service.ngsummary.json
β β β βββ contacts-routing.module.js
β β β βββ contacts-routing.module.js.map
β β β βββ contacts-routing.module.metadata.json
β β β βββ contacts-routing.module.ngfactory.js
β β β βββ contacts-routing.module.ngfactory.js.map
β β β βββ contacts-routing.module.ngsummary.json
β β β βββ contacts.module.js
β β β βββ contacts.module.js.map
β β β βββ contacts.module.metadata.json
β β β βββ contacts.module.ngfactory.js
β β β βββ contacts.module.ngfactory.js.map
β β β βββ contacts.module.ngsummary.json
β β β βββ contacts.service.js
β β β βββ contacts.service.js.map
β β β βββ contacts.service.metadata.json
β β β βββ contacts.service.ngfactory.js.map
β β β βββ contacts.service.ngsummary.json
β β βββ exception
β β β βββ 403.component.js
β β β βββ 403.component.js.map
β β β βββ 403.component.metadata.json
β β β βββ 403.component.ngfactory.js
β β β βββ 403.component.ngfactory.js.map
β β β βββ 403.component.ngsummary.json
β β β βββ 404.component.js
β β β βββ 404.component.js.map
β β β βββ 404.component.metadata.json
β β β βββ 404.component.ngfactory.js
β β β βββ 404.component.ngfactory.js.map
β β β βββ 404.component.ngsummary.json
β β β βββ 500.component.js
β β β βββ 500.component.js.map
β β β βββ 500.component.metadata.json
β β β βββ 500.component.ngfactory.js
β β β βββ 500.component.ngfactory.js.map
β β β βββ 500.component.ngsummary.json
β β βββ route-routing.module.js
β β βββ route-routing.module.js.map
β β βββ route-routing.module.metadata.json
β β βββ route-routing.module.ngfactory.js
β β βββ route-routing.module.ngfactory.js.map
β β βββ route-routing.module.ngsummary.json
β β βββ route.module.js
β β βββ route.module.js.map
β β βββ route.module.metadata.json
β β βββ route.module.ngfactory.js
β β βββ route.module.ngfactory.js.map
β β βββ route.module.ngsummary.json
β β βββ index.js
β β βββ index.js.map
β β βββ index.metadata.json
β β βββ index.ngfactory.js
β β βββ index.ngfactory.js.map
β β βββ index.ngsummary.json
β β βββ shared.module.js
β β βββ shared.module.js.map
β β βββ shared.module.metadata.json
β β βββ shared.module.ngfactory.js
β β βββ shared.module.ngfactory.js.map
β β βββ shared.module.ngsummary.json
β βββ app.component.js
β βββ app.component.js.map
β βββ app.component.metadata.json
β βββ app.component.ngfactory.js
β βββ app.component.ngfactory.js.map
β βββ app.component.ngsummary.json
β βββ app.module.js
β βββ app.module.js.map
β βββ app.module.metadata.json
β βββ app.module.ngfactory.js
β βββ app.module.ngfactory.js.map
β βββ app.module.ngsummary.json
βββ environments
β βββ environment.js
β βββ environment.js.map
β βββ environment.metadata.json
β βββ environment.ngsummary.json
β βββ environment.prod.js
β βββ environment.prod.js.map
β βββ environment.prod.metadata.json
β βββ environment.prod.ngsummary.json
βββ main.js
βββ main.js.map
βββ main.ngsummary.json
βββ polyfills.js
βββ polyfills.js.map
βββ polyfills.ngsummary.json
```

`app.component.ngfactory.js`

```js
/**
 * @fileoverview This file was generated by the Angular template compiler. Do not edit.
 *
 * @suppress {suspiciousCode,uselessCode,missingProperties,missingOverride,checkTypes}
 * tslint:disable
 */

// import * as i0 from "@angular/core";
// import * as i1 from "@angular/router";
// import * as i2 from "./app.component";
// var styles_AppComponent = [];
// var RenderType_AppComponent = i0.Ι΅crt({ encapsulation: 2, styles: styles_AppComponent, data: {} });
// export { RenderType_AppComponent as RenderType_AppComponent };
// export function View_AppComponent_0(_l) { return i0.Ι΅vid(0, [(_l()(), i0.Ι΅eld(0, 16777216, null, null, 1, "router-outlet", [], null, null, null, null, null)), i0.Ι΅did(1, 212992, null, 0, i1.RouterOutlet, [i1.ChildrenOutletContexts, i0.ViewContainerRef, i0.ComponentFactoryResolver, [8, null], i0.ChangeDetectorRef], null, null)], function (_ck, _v) { _ck(_v, 1, 0); }, null); }
// export function View_AppComponent_Host_0(_l) { return i0.Ι΅vid(0, [(_l()(), i0.Ι΅eld(0, 0, null, null, 1, "app-root", [], null, null, null, View_AppComponent_0, RenderType_AppComponent)), i0.Ι΅did(1, 114688, null, 0, i2.AppComponent, [], null, null)], function (_ck, _v) { _ck(_v, 1, 0); }, null); }
// var AppComponentNgFactory = i0.Ι΅ccf("app-root", i2.AppComponent, View_AppComponent_Host_0, {}, {}, []);
// export { AppComponentNgFactory as AppComponentNgFactory };
//# sourceMappingURL=app.component.ngfactory.js.map
```

```js
/**
 * @fileoverview This file was generated by the Angular template compiler. Do not edit.
 *
 * @suppress {suspiciousCode,uselessCode,missingProperties,missingOverride,checkTypes}
 * tslint:disable
 */

// import * as i0 from "@angular/core";
// import * as i1 from "@angular/router";
// import * as i2 from "./app.component";
// var styles_AppComponent = [];
// var RenderType_AppComponent = i0.Ι΅crt({ encapsulation: 2, styles: styles_AppComponent, data: {} });
// export { RenderType_AppComponent as RenderType_AppComponent };
// export function View_AppComponent_0(_l) { return i0.Ι΅vid(0, [(_l()(), i0.Ι΅eld(0, 16777216, null, null, 1, "router-outlet", [], null, null, null, null, null)), i0.Ι΅did(1, 212992, null, 0, i1.RouterOutlet, [i1.ChildrenOutletContexts, i0.ViewContainerRef, i0.ComponentFactoryResolver, [8, null], i0.ChangeDetectorRef], null, null)], function (_ck, _v) { _ck(_v, 1, 0); }, null); }
// export function View_AppComponent_Host_0(_l) { return i0.Ι΅vid(0, [(_l()(), i0.Ι΅eld(0, 0, null, null, 1, "app-root", [], null, null, null, View_AppComponent_0, RenderType_AppComponent)), i0.Ι΅did(1, 114688, null, 0, i2.AppComponent, [], null, null)], function (_ck, _v) { _ck(_v, 1, 0); }, null); }
// var AppComponentNgFactory = i0.Ι΅ccf("app-root", i2.AppComponent, View_AppComponent_Host_0, {}, {}, []);
// export { AppComponentNgFactory as AppComponentNgFactory };
//# sourceMappingURL=app.component.ngfactory.js.map
```

```js
/**
 * @fileoverview This file was generated by the Angular template compiler. Do not edit.
 *
 * @suppress {suspiciousCode,uselessCode,missingProperties,missingOverride,checkTypes}
 * tslint:disable
 */

// import * as i0 from "@angular/core";
// import * as i1 from "@angular/router";
// import * as i2 from "./app.component";
// var styles_AppComponent = [];
// var RenderType_AppComponent = i0.Ι΅crt({ encapsulation: 2, styles: styles_AppComponent, data: {} });
// export { RenderType_AppComponent as RenderType_AppComponent };
// export function View_AppComponent_0(_l) { return i0.Ι΅vid(0, [(_l()(), i0.Ι΅ted(-1, null, [" hi,brother "])), (_l()(), i0.Ι΅eld(1, 16777216, null, null, 1, "router-outlet", [], null, null, null, null, null)), i0.Ι΅did(2, 212992, null, 0, i1.RouterOutlet, [i1.ChildrenOutletContexts, i0.ViewContainerRef, i0.ComponentFactoryResolver, [8, null], i0.ChangeDetectorRef], null, null)], function (_ck, _v) { _ck(_v, 2, 0); }, null); }
// export function View_AppComponent_Host_0(_l) { return i0.Ι΅vid(0, [(_l()(), i0.Ι΅eld(0, 0, null, null, 1, "app-root", [], null, null, null, View_AppComponent_0, RenderType_AppComponent)), i0.Ι΅did(1, 114688, null, 0, i2.AppComponent, [], null, null)], function (_ck, _v) { _ck(_v, 1, 0); }, null); }
// var AppComponentNgFactory = i0.Ι΅ccf("app-root", i2.AppComponent, View_AppComponent_Host_0, {}, {}, []);
// export { AppComponentNgFactory as AppComponentNgFactory };
//# sourceMappingURL=app.component.ngfactory.js.map
```

#### packagesπ

##### webpack

packages/ngtools/webpack

##### β­schematics

##### ng_packagr

packages/angular_devkit/build_ng_packagr/src/build/index.ts

---

##### wtf with ngc ngcc

https://medium.com/angular-in-depth/a-deep-deep-deep-deep-deep-dive-into-the-angular-compiler-5379171ffb7a
