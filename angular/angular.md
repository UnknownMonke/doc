# Angular Basics

### Summary

- [Overview](#overview)
- [Releases & support cycle](#releases--support-cycle)
- [Configuration](#configuration)
- [Decorator](#decorator)
- [Module](#module)
- [Component](#domponent)
- [Standalone components](#standalone-components)
    - [Loading Strategies](#loading-strategies)
    - [Data Binding](#data-binding)
    - [Change Detection](#change-detection)
- [Pipe](#pipe)
- [Directive](#directive)
    - [Attribute directive](#attribute-directive)
    - [Structural directive](#structural-directive)
- [Services](#services)
- [Dependency Injection](#dependency-injection)
    - [Injector](#injector)
- [Lifecycle Hooks](#lifecycle-hooks)
- [Immutability](#immutability)
- [Router](#router)
- [Signals](#signals)
- [Internationalization](#internationalization)
    - [Setup](#setup)
    - [Preparing components for translation](#preparing-components-for-translation)
    - [Metadata](#metadata)
    - [Translation files](#translation-files)
- [Animations](#animations)
- [Images](#images)

#
<br>

## Overview

- First release in 2009.

- *MIT license*.

- <u>Framework</u> and <u>development platform</u> to build **scalable**, **single-page** web applications :

    - Content updates dynamically without refreshing the browser.

- Emphasizes a separation between HTML templates and Javascript, and the use of custom attributes and dynamic content.

- Avoids embedding templates inside Javascript files and **manipulating the DOM directly** (jQuery, other frameworks...).

- Written in TypeScript.

- <u>Embedded tools</u> : 

    - **Angular CLI** (follows major versions) - `ng` command tool.
    - **Angular Language Service**.
    - **Angular Dev Tools** : real-time debugging infos.
    - **Angular Schematics** : custom reusable code across projects.

- Implements core and optional functionalities as a set of TypeScript libraries that can be imported into applications.

- **Ahead-Of-Time** (AOT) compilation supported for production since Angular 8.

#
### Releases & support cycle.

- **Semantic versioning** :

    - <u>Major releases</u> :

        - Big new features.
        - Every *6 months*.
        - Update guide provided.

    - <u>Minor releases</u> :

        - Small new features.
        - Backward compatible.

    - <u>Patch releases</u> :

        - Low risk fixes for bugs & security.

<br>

- Major releases are supported for *18 months* :

    - 6 months of **active support** (minor, patch releases).
    - 12 months of **long-term support** (only patch releases).

<br>

## Configuration

Angular uses **webpack** & webpack configuration options.

`tsconfig.json`

- Compiler options for typescript and Angular specifics.

`angular.json`

- Main CLI config file. Extends and contains **webpack configuration parameters** :

    - Environment variables.
    - Schematics.
    - Profiles.
    - ...

<br>

## Decorator

- Analog to **Spring annotations**.

- Functions that returns functions.

- Provides **metadata** about the code.

- Marked using '**@**' symbol.

- Invoked at **runtime** with arguments.

- **Common decorators** :

    - `@NgModule()` - Modules.
    - `@Component()` - Components.
    - `@Injectable()` - Services.
    - `@Pipe()` - Pipes.
    - `@Directive()` - Directives.
    - `@Input()` - Incoming component data flow.
    - `@Output()` - Outcoming component data flow.

<br>

## Module

A collection of files that work together (components, services, pipes...).

Decorator properties (all properties are **optional**) :

`declarations`

- All components, directives & pipes belonging to the module.

`imports`

- External modules dependencies.

`exports`

- Files exposed to other modules.

`providers`

- Files exposed to the dependency injector.

`bootstrap`

- Specifies a component to load first at startup (usually the root component).

<br>

## Component

Main building block.

- Contains :

    - **HTML template** - declares what renders on the page.
    - Optional **CSS style** applied to the template.
    - **Typescript class** - defines behavior.
    - **Component selector** - defines how the component is used in a template.

<br>

A template combines ordinary HTML with Angular directives and binding markup that allow Angular to modify the HTML before rendering it for display.

- Usages :

    - Build **pages**.
    - Build **reusable** parts.
    - Build feature **logic**.

- Components define **views** :

    - Sets of screen elements that Angular can choose among and modify according to the program logic and data.

- Components use **services** :

    - Provides background functionality not directly related to views such as fetching data and processing business logic. 

    - Can be injected into components as **dependencies**, making the code *modular*, *reusable*, and *efficient*.

<br>

> Unless they are *standalone*, components should be hosted within their own module to clearly define their dependencies and scope.

#
### Standalone components

- Must declare its own imports & providers.

- Removes module boilerplate code.

- Backward compatible with modules : can be imported within modules like a module.

#
### Loading Strategies

**Eager-loading**

- Loads modules as soon as possible (startup).

**Lazy-loading**

- Only loads modules when needed (after resolving route).

- Faster initial page load.

- More network lag between pages as modules are loaded.

**Preloading**

- Loaded modules make calls to load children in the background.

- Usually combined with lazy-loading to avoid lag when navigating.

*Ex :*

``` typescript
export class PreloadingService implements PreloadingStategy {
    
    public preload(route: Route, fn: () => Observable<any>): Observable<any> {
        return (route.data && route.data['preload']) ? fn() : of(null);
    }
}
```
#
### Data Binding

Allows applications to display data values to the client and respond to user actions.

- Declares the relationship between a DOM attribute and a data source and let the framework handle the details. 

- Alternative to manually attaching event listeners and pushing, pulling and updating values into the HTML.

- The `NgNonBindable` directive :
    
    - Disables binding, interpolation and directives in the element and all its children.

*Ex :*

``` html
<input type="text" class="form-control" #filter (keyup)="update(filter.value)">
<button (click)="update(''); filter.value=''" [applOnlineStatus]="player.online">Clear {{ player.name }}</button>
```

- **Template reference variables** : `#<template_name>` will reference the template, directly giving access to its DOM properties.

- **Event binding** : DOM events can be accessed using parenthesis.

- **Property binding** : Custom properties can be created using brackets. Angular will set the value dynamically at runtime.

- **Interpolation** : Displays dynamic content as text between double braces.

#
### Change Detection

Synchronization mechanism between the state of the DOM and the state of the data. 

**Motivations**

- The underlying data is updated by the server : the displayed data in the DOM isn't up-to-date anymore. 
- The user interacts with the UI : the underlying data isn't up-to-date anymore.

An **update** is needed to resync the view with the underlying model.

**Values**

- `Default` :

    - Runs everytime a DOM action is performed, or a value has changed in strings, arrays, ...
    - Goes through **every component** of the tree and checks **every data-bound property** to compare with the previous state, then updates to reflect any new data value.

- `OnPush` :

    - Only runs when **explicitly invoked**, or when a data bound attribute changes, such as an input or the value emitted by a **publisher**.
    - Does not parse the whole component tree each time.
    - Improves **performances**.

<br>

> The change detection should always be set to `OnPush`.

<br>

## Pipe

**Transforms** input values for display (*currency*, *dates*...).

- Can be chained.
- Can have arguments.

*Ex :*

``` html
<span>{{ player.score | percent | slice : 0 : 5 }}</span>
```
<br>

- **Pure pipes** : always return the same output for the same input.

    - Makes change detection faster.
    - Angular only **compares by reference** to gain speed.
    - A pure pipe *will not work for nested objects and arrays*.

- Can be marked as **impure** : will be run at each change detection.

- **Built-in** pipes :

| Class         | Details                                                                      |
|---------------|------------------------------------------------------------------------------|
| DatePipe      | Formats a date value according to **locale** rules.                          |
| CurrencyPipe  | Number to currency string, formatted according to locale rules.              |
| DecimalPipe   | Number to string with a decimal point, formatted according to locale rules.  |
| PercentPipe   | Number to percentage string, formatted according to locale rules.            |
| AsyncPipe     | Subscribes and unsubscribes to an asynchronous source such as an observable. |
| JsonPipe      | Displays a component object property to the screen as JSON for debugging.    |
| UpperCasePipe |                                                                              |
| LowerCasePipe |                                                                              |

<br>

## Directive

Can modify the DOM structure, attributes or component data model.

- Usually associated with an HTML element or attribute, which is often referred to as the directive itself. 

- When Angular finds a directive in an HTML template, it creates the matching directive class instance and gives it control over that portion of the DOM.

<br>

**<u>Types of directives</u>** :

- **[Components](#components)** - Injects a template into the DOM.

- **Attribute directives** - Modifies behavior and appearance of page elements.

- **Structural directives** - Modifies the structure of the DOM.

#
### Attribute directive

Modifies behavior and appearance of page elements.

**Built-in** directives :

| Name        | Details                                            |
|-------------|----------------------------------------------------|
| **NgClass** | Adds and removes a set of CSS classes.             |
| **NgStyle** | Adds and removes a set of HTML styles.             |
| **NgModel** | Adds two-way data binding to an HTML form element. |

<br>

*Ex :*

``` typescript
@Directive({
    standalone: true,
    selector: "[appHighlight]",
})
export class HighlightDirective {
    constructor(private el: ElementRef) {}

    @Input() defaultColor = "";
    @Input() appHighlight = "";

    @HostListener("mouseenter") onMouseEnter() {
        this.highlight(this.appHighlight || this.defaultColor || "red");
    }

    @HostListener("mouseleave") onMouseLeave() {
        this.highlight('');
    }

    private highlight(color: string) {
        this.el.nativeElement.style.backgroundColor = color;
    }
}
```
<br>

<img src="assets/ng_directive.gif" alt="drawing" width="300"/>

<br>

#
### Structural directive

Changes the DOM layout by adding and removing DOM elements.

**Built-in** directives :

| Name         | Details                                                          |
|--------------|------------------------------------------------------------------|
| **NgIf**     | Conditionally creates or disposes of subviews from the template. |
| **NgFor**    | Repeat a node for each item in a list.                           |
| **NgSwitch** | A set of directives that switch among alternative views.         |

<br>

*Ex :*

``` html
<!-- Shorthand syntax. -->
<div *ngIf="hero" class="name">{{ hero.name }}</div>

<ng-template [ngIf]="hero">
    <div class="name">{{ hero.name }}</div>
</ng-template>
```
``` html
<!-- Shorthand syntax. -->
<div *ngFor="let hero of heroes; let i=index; let odd=odd; trackBy: trackById" [class.odd]="odd">
    ({{ i }}) {{ hero.name }}
</div>

<ng-template ngFor let-hero [ngForOf]="heroes" let-i="index" let-odd="odd" [ngForTrackBy]="trackById">
    <div [class.odd]="odd">
        ({{ i }}) {{ hero.name }}
    </div>
</ng-template>
```
- `ng-template` doesn't render by default, but needs a **trigger** directive or pipe.

<br>

## Services

- Holds processes that do not directly **change the view**.

- Should hold business logic to keep components **simple**.

- `@Injectable()` registers the service to the injector via a token (usually the class).

<br>

## Dependency Injection

Core design concept.

- Classes with decorators can configure **dependencies** that they need.

- 2 main roles :

    - Dependency **consumer**.
    - Dependency **provider**.

#
### Injector

Abstraction that facilitates the interaction between dependency consumers and dependency providers.

- When a class is invoked in a contructor, returns the corresponding instance if exists.

- If not, a new instance is created and stored in the **registry**.

- Angular creates an **application-wide injector** (also known as *root* injector) during the application bootstrap process, as well as any other injectors as needed.

<br>

*Ex :*

- Registering and providing a service :

    ``` typescript
    @Injectable({
        providedIn: 'root'
    })
    class MyService {
        // ...
    }
    ```
    - The "root" attributes registers into the root injector as a **singleton**. This is the default behavior.
    - Root services do not need to be consumed in the `providers` array.

<br>

- Consuming the service in component :

    ``` typescript
    @Component({
        standalone: true,
        selector: 'my-list',
        template: '...',
        providers: [MyService] // Shorthand syntax.
    })
    class MyComponent {
        // ...
    }
    ```
    ``` typescript
    @Component({
        standalone: true,
        selector: 'my-list',
        template: '...',
        providers: [
            // Provider configuration object if the token is different from the class.
            { provide: MyService, useClass: MyService }
        ]
    })
    class MyComponent {
        // ...
    }
    ```
<br>

- Injecting the service in component :

    ``` typescript
    @Component({ /* ... */ })
    class MyComponent {
        constructor(
            private service: MyService // Constructor injection.
        ) {}
        // ...
    }
    ```
    ``` typescript
    @Component({ /* ... */ })
    class MyComponent {
        private service = inject(MyService); // Field injection.
    }
    ```
<br>

## Lifecycle Hooks

Interface that allows to hook into the lifecycle of directives & components as they are created, updated and destroyed, to perform specific logic.

Each interface contains a single method prefixed with `ng`.

| Method                    | Details                                         |
|---------------------------|-------------------------------------------------|
| **ngOnChanges**           | When an input or output binding value changes.  |
| **ngOnInit**              | After the first ngOnChanges.                    |
| **ngDoCheck**             | Developer's custom change detection.            |
| **ngAfterContentInit**    | After component content initialized.            |
| **ngAfterContentChecked** | After every check of component content.         |
| **ngAfterViewInit**       | After the views of a component are initialized. |
| **ngAfterViewChecked**    | After every check of the views of a component.  |
| **ngOnDestroy**           | Just before the directive is destroyed.         |

<br>

## Immutability

Inability to alter the state of a value after its creation. 

**Reactive forms** perform immutable changes :
Each change to the data model produces a new data model rather than modifying the existing one.

**Template-driven forms** perform mutable changes with NgModel and two-way data binding to modify the existing data model in place.

<br>

## Router

`loadComponent` / `loadChildren`

- Specifies a callback of components / modules imports to load after route completion.
- Enables **lazy-loading** of components & modules.

<br>

- Activating routes :

    - `RouterModule.forRoot` to define routes for the application (in root module).
    - `RouterModule.forChild` to define routes for a submodule only.

- Accessing route params inside route definition :

``` typescript
{
    path: "profile/:id",
    loadComponent: () => import('./profile.component').then(m => m.ProfileComponent),
    title: (route: ActivatedRouteSnapshot) => `Profile for ${route.paramMap.get('id')}`
}
```
<br>

## Signals

- Angular own approach to **state management**.

- Largely inspired from **ngRx** and **RxJs** :

    - **Pub/Sub Observable** implementation from within Angular.
    - Alernative to `Subject` and `BehaviorSubject`.

- More efficient than `OnPush` change detection :

    - Wraps data inside getters and setters that can easily be tracked.

- **Getter by default** : calling the signal will return its value.

*Ex :*

``` typescript
const value: Message[] = signal();
```
<br>

- `set` - sets the value directly.

- `mutate` - changes the data in place.

- `update` - returns a new mutated value using previous value.

<br>

- **Computed signals** :

    - **Reducers** : read-only signal with value computed from previous signals.
    - Lazy-evaluated.
    - Memoized.

- **Effects** :

    - Operation that runs whenever one or more signal values **change**.
    - Can process values from *different parts of the state* altogether.
    - **Side-effect** : triggers other processes when the value change.
    - Always **asynchronous**.
    - Need to **access dependencies** : should be set inside the constructor.

<br>

## Internationalization

- Also known as **i18n**.

- Process of designing and preparing the project for use in **different locales**.

    - Extracts text for translation into different languages.
    - Formats data for a specific locale (currencies, dates...).

- A **locale** is referenced by its *Unicode identifier* : `<language_id>-<locale_extension>`.

    *Ex :* 

    | Language | Locale | Unicode locale ID |
    |----------|--------|-------------------|
    | English  | Canada | `en-CA`           |
    | English  | USA    | `en-US`           |
    | French   | Canada | `fr-CA`           |
    | French   | France | `fr-FR `          |

<br>

- `Date` and `Currency` pipes use the current locale to format values. A specific locale can also be specified.

- Built-in feature of Angular : no need to use external libraries such as `ngx-translate` (deprecated) anymore.

- Caveat : no live language change is possible as the locale needs to be recompiled.

#
### Setup

- Add the `localize` package :

> `ng add @angular/localize`

- Prepare components for translation.

- Extract marked text into a **source language file**.

- Add translations files to a destination folder.

- Specify a locale ID for the code to use in **Angular.json**, and locales used for the application.

``` json
"i18n": {
    "sourceLocale": "en-US",
    "locales": {
        "fr": {
            "translation": "src/locale/messages.fr.json",
        },
        // ...
    }
}
```
<br>

- Multiple locales can be built and deployed under multiple dist directories and accessible under `app/<locale>` from the browser. 

#
### Preparing components for translation

- Text can be marked in component template :

    ``` html
    <h1 i18n>Hello i18n!</h1>
    ```
- Elements attributes can be marked for translation :

    ``` html
    <img [src]="/logo" i18n-title title="Angular logo" alt="Angular logo">
    ```    
- Text can be marked in component code :

    ``` typescript
    $localize `dashboard`;
    ```
- Metadata can be specified if necessary.

#
### Metadata

| Parameter       | Details                                                                 |
|-----------------|-------------------------------------------------------------------------|
| **Custom ID**   | Provides a custom identifier.                                           |
| **Description** | Provides additional information or context.                             |
| **Meaning**     | Provides the meaning or intent of the text within the specific context. |

<br>

- Syntax : `:<meaning>|<description>@@<custom_id>:<text>`.

- The *Angular extraction tool* generates a translation unit entry for each i18n attribute in a template.

- Each entry gets assigned an **unique ID** based on the *meaning* and *description*.

- The same text elements with different meanings are extracted with **different IDs**.

<br>

*Ex :*

``` typescript
$localize `:correct:right`;
$localize `:direction:right`;
```
The string 'right' will generate 2 translations entries since different meanings are specified.

#
### Translation files

- `ng extract-i18n` will extract a `messages.xlf` source language file.

| Command option   | Details                            |
|------------------|------------------------------------|
| `--format`       | Output file format (json, xml...). |
| `--out-file`     | Output file name.                  |
| `--output-path ` | Output directory.                  |

<br>

- Translation files can be created from copies of the source file.

<br>

## Animations

- Animates css elements from component typescript code.

- Requires `@angular/animations` and `@angular/platform-browser`.

- Bootstrap :

    - **Component-based**

    ``` typescript
    bootstrapApplication(AppComponent, {
        providers: [
            // provideAnimations() if animations should play on bootstrap directly.
            provideAnimationsAsync(),
        ]
    });    
    ```
    - **Module-based**

    ``` typescript
    @NgModule({
        imports: [BrowserModule, BrowserAnimationsModule],
        declarations: [],
        bootstrap: [],
    })
    export class AppModule {}   
    ```
<br>

- Holds **built-in animations**.

- Can create **custom animations**.

<br>

*Ex :*

``` typescript
@Component({
  standalone: true,
  selector: 'app-open-close',
  animations: [
    trigger('openClose', [
        state(
            'open',
            style({
                height: '200px',
                opacity: 1,
                backgroundColor: 'yellow',
            })
        ),
        state(
            'closed',
            style({
                height: '100px',
                opacity: 0.8,
                backgroundColor: 'blue',
            })
        ),
        transition('open => closed', [animate('1s')]),
        transition('closed => open', [animate('0.5s')])
    ]),
  ],
  template: `
    <nav>
        <button type="button" (click)="toggle()">Toggle Open/Close</button>
    </nav>
    <div [@openClose]="isOpen ? 'open' : 'closed'" class="open-close-container">
        <p>The box is now {{ isOpen ? 'Open' : 'Closed' }}!</p>
    </div>
  `
})
export class OpenCloseComponent {
    isOpen = true;
    toggle() {
        this.isOpen = !this.isOpen;
    }
}
```
<br>

## Images

Performance best practices for loading images using the `NgOptimizedImage` directive.

- Loading of the **Largest Contentful Paint (LCP)** image prioritized by :


    - Automatically setting the `fetchpriority` attribute on the `<img>` tag.
    - Lazy loading other images by default.
    - Automatically generating a preconnect link tag in the document head.
    - Automatically generating a `srcset` attribute.
    - Generating a preload hint if app is using SSR.

- Also enforces best practices :

    - Uses image **CDN urls** to apply optimizations.
    - Prevents layout shift by requiring `width` and `height`.
    - Warns if width or height have been set incorrectly.
    - Warns if the image will be visually distorted when rendered.

<br>

*Ex :*

The LCP is marked using the `priority` attribute :

``` html
<img ngSrc="cat.jpg" width="400" height="200" priority>
```
Background image can be achieved using `fill` instead of specifying width and height :

``` html
<!-- Positioned element only. -->
<img ngSrc="cat.jpg" fill>    
```


