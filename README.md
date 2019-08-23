# ngx-autofocus-fix

Angular 5+ directive for fix autofocus on dynamically created controls (`*ngIf`, `*ngFor`, etc.).

![Autofocus Demo](demo.gif)

## Advantages over other libraries

* **Uses native HTML attribute `autofocus` as the selector!**  
* There are no custom selectors, no need to change your HTML template.
* Works with native DOM. Doesn't use any dependencies(jQuery, lodash, etc.).
* 100% Coverage, over 60 unit tests.
* E2E tests for 8,7,6 and 5 versions of Angular including e2e test for Angular Material Input.
* The library understands an extensive list of input data. (`null/NaN/'true'/[]/...`, not only boolean). See [Advanced examples](#advanced-examples)
* Supports asynchronous focusing (Useful for infinite scroll).
* Works perfectly with Angular Material. (there is an E2E test)
* Works with AOT mode.
* Configurable. Use can use input attributes or provide global options via `AutofocusFixConfig`

## Installation

To install this library, run:

```bash
$ npm i ngx-autofocus-fix --save
```
or
```bash
$ yarn add ngx-autofocus-fix
```

## Quick start

1. Import the library in your Angular application, for example in `AppModule`:

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AutofocusFixModule } from 'ngx-autofocus-fix'; // <--- new code

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent,
  ],
  imports: [
    BrowserModule,

    AutofocusFixModule, // <--- new code
  ],
  providers: [],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

2. You can now use autofocus directive in app.component.html

```html
<input autofocus
       placeholder="I have autofocus"
       *ngIf="showInput"
>
<button (click)="showInput = !showInput">Toggle Input</button>
```

## Online demos:**

* [The simplest case](...)
* [Smart mode](...)
* [Global config (`AutofocusFixConfig`) - simple example](...)
* [Complex example (Angular Material, Infinite scroll, Multiple global configs)](...)

## Advanced examples

Ways to **disable autofocus:** any js-falsy value, except an empty string

```html
   <!-- with data binding -->
   <input [autofocus]=""> <!-- undefined value -->
   <input [autofocus]="undefined">
   <input [autofocus]="false">
   <input [autofocus]="null">
   <input [autofocus]="0">
   <input [autofocus]="NaN">
   
   <!-- without data binding -->
   <input autofocus="undefined">
   <input autofocus="false">
   <input autofocus="null">
   <input autofocus="0">
   <input autofocus="NaN">
   
   <input> <!-- disabled by default -->
``` 

Ways to **enable autofocus:** any js-truthy value and an empty string

```html
   <!-- an empty string will enable autofocus, this is default HTML behavior -->
   <input [autofocus]="''">
   <input autofocus="">
   <input autofocus> <!-- this is an empty string too -->
   
   <input autofocus="autofocus">
   
   <input [autofocus]="true">
   <input [autofocus]="1">
   <input autofocus="true">
   
   <input [autofocus]="'any other values'">
   <input autofocus="any other values">

   <input [autofocus]="{}">
   <input [autofocus]="[]">
```

## Input's Smart Empty Check normalization mode

All input values are passed through the function: `normalizeInputAsBoolean(value: any, smartEmptyCheck = false): boolean`.

Smart Empty Check mode changes the behavior so that the following values are treated as falsy:
* An empty string `''`
* An empty object `{}`
* An empty array `[]`

See [Configuration](#configuration) to understand how to enable the mode.

**Notes:**
* Smart Empty Check normalization mode available only for `autofocus` attribute. All other directive `@Input`'s always works in the default normalization mode.
* Using attribute `autofocus` without any value doesn't enable autofocusing in Smart Empty Check mode. Because of an empty value means an empty string in terms of Angular templates syntax. 

## Configuration

**There are three ways to change the `AutofocusFixDirective`:**  
### 1. Specify attribute-options for specific HTML Element
   ```html
   <input type="text"
          autofocus
          autofocusFixAsync
   >
   ```
TODO: finish
### 2. Specify global options for the whole application by passing it to `.forRoot({ ... })`
TODO: finish
### 3. Provide Lazy-Route level or Component level config `new AutofocusFixConfig({ ... })`
TODO: finish

## Development
TODO: finish

To generate all `*.js`, `*.d.ts` and `*.metadata.json` files:

```bash
$ npm run build
```

To lint all `*.ts` files:

```bash
$ npm run lint
```

## License

MIT © [Anton Korniychuk](mailto:dev@korniychuk.pro)
