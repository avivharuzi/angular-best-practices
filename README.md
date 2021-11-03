# Angular Best Practices

[![Angular](assets/angular.png)](https://angular.io)

Angular guide for teams that look for consistency through best practices.

## Table of Contents

1. [Single Responsibility Principle](#single-responsibility-principle)
1. [Follow Consistent Angular Coding Styles](#follow-consistent-angular-coding-styles)
1. [Keep Up to Date](#keep-up-to-date)
1. [Strict Mode](#strict-mode)
1. [Use Angular CLI](#use-angular-cli)
1. [Use State Management](#use-state-management)
1. [Use Environment Variables](#use-environment-variables)
1. [Divide Imports](#divide-imports)
1. [Prefer Observables Over Promises](#prefer-observables-over-promises)
1. [Component Properties and Methods Order](#component-properties-and-methods-order)
1. [Lifecycle Hooks Interfaces and Order](#lifecycle-hooks-interfaces-and-order)
1. [Write Logic Outside Lifecycle Hook](#write-logic-outside-lifecycle-hook)
1. [Component Event Names Rules](#component-event-names-rules)
1. [HTML Wrapping and Order](#html-wrapping-and-order)
1. [Wrap Pipes Within Parenthesis](#wrap-pipes-within-parenthesis)
1. [Avoid Logic in Templates](#avoid-logic-in-templates)
1. [Prevent Memory Leaks](#prevent-memory-leaks)
1. [Subscribe in Template Using async Pipe](#subscribe-in-template-using-async-pipe)
1. [Use Change Detection OnPush](#use-change-detection-onpush)
1. [Avoid Having Subscriptions Inside Subscriptions](#avoid-having-subscriptions-inside-subscriptions)
1. [Use trackBy Along With ngFor](#use-trackby-along-with-ngfor)
1. [Strings Should Be Safe](#strings-should-be-safe)
1. [Avoid any Type](#avoid-any-type)
1. [Use Mandatory Inputs](#use-mandatory-inputs)
1. [Do Not Pass Streams to Components Directly](#do-not-pass-streams-to-components-directly)
1. [Do Not Pass Streams to Services](#do-not-pass-streams-to-services)
1. [Do Not Expose Subjects](#do-not-expose-subjects)
1. [Handle RxJS Errors](#handle-rxjs-errors)
1. [Avoid Changing the DOM Directly](#avoid-changing-the-dom-directly)
1. [Avoid Computing Values in the Template](#avoid-computing-values-in-the-template)
1. [Use Immutability](#use-immutability)
1. [Safe Navigation Operator in HTML Template](#safe-navigation-operator-in-html-template)
1. [Break Down Into Small Reusable Components](#break-down-into-small-reusable-components)
1. [Use Smart and Dumb Components](#use-smart-and-dumb-components)
1. [Use Lazy Loading](#use-lazy-loading)
1. [Use index.ts](#use-index.ts)
1. [Isolate API Hacks](#isolate-api-hacks)
1. [Cache API Calls](#cache-api-calls)
1. [Use CDK Virtual Scroll](#use-cdk-virtual-scroll)
1. [Use Angular Service Workers and PWA](#use-angular-service-workers-and-pwa)
1. [Use Angular Universal](#use-angular-universal)
1. [Use Lint Rules](#use-lint-rules)

## Single Responsibility Principle

It is very important not to create more than one component, service, directive… inside a single file. Every file should be responsible for a **single functionality**.

***Why?***: By doing this, we are keeping our files clean, readable, and maintainable.

**[Back to top](#table-of-contents)**

## Follow Consistent Angular Coding Styles

Here are some set of rules we need to follow to make our project with the proper coding standard.

* Limit files to 400 Lines of code.
* Define small functions and limit them to no more than 75 lines.
* Have consistent names for all symbols. The recommended pattern is `feature.type.ts`.
* If the values of the variables are intact, then declare it with `const`.
* Use `dashes` to separate words in the descriptive name and use `dots` to separate the descriptive name from the type, for example: `movie-list.component.ts`.
* Names of properties and methods should always be in lower camel case. 
* Always leave one empty line between imports and modules, such as third party and application imports and third-party modules and custom modules.

For more information read it on [Angular coding style guide](https://angular.io/guide/styleguide)

**[Back to top](#table-of-contents)**

## Keep Up to Date

Angular follows semantic versioning with a new major version released every six months.

Semantic versioning is a convention used for versioning software. It has a `major.minor.patch` format. Angular increments each part when they release `major`, `minor`, or `patch` changes.

You can follow the news about the latest version of Angular from the [CHANGELOG](https://github.com/angular/angular/blob/master/CHANGELOG.md) and make sure you keep your Angular version up to date, ensuring you always get the latest features, bug fixes, and performance enhancements like Ivy.

It would help if you also used [this official tool](https://update.angular.io) when updating your project from one version to the next.

**[Back to top](#table-of-contents)**

## Strict Mode

The Angular team has moved to apply the strict mode progressively with an option in Angular 10.

From Angular 12 all projects are starting with strict mode enabled by default.

You should check your project is using strict mode and if not update it to use strict mode.

**Why?**: You’ll benefit from the TypeScript’s type system in your templates and gain best practices rules from Angular team. 

```json
{
  "compilerOptions": {
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  },
  "angularCompilerOptions": {
    "enableI18nLegacyMessageIdFormat": false,
    "strictInjectionParameters": true,
    "strictInputAccessModifiers": true,
    "strictTemplates": true
  }
}
```

**[Back to top](#table-of-contents)**

## Use Angular CLI

[Angular CLI](https://angular.io/cli) is one of the most powerful accessibility tools available when developing apps with Angular. Angular CLI makes it easy to create an application and follows all the best practices! Angular CLI is a command-line interface tool that is used to initialize, develop, scaffold, maintain and even test and debug Angular applications.

So instead of creating the files and folders manually, use Angular CLI to generate new `components`, `directives`, `modules`, `services`, `pipes`, etc.

```shell
# Install Angular CLI
npm i -g @angular/cli

# Check Angular CLI version
ng version
```

**[Back to top](#table-of-contents)**

## Use State Management

One of the most challenging things in software development is state management. State management in Angular helps in managing state transitions by storing the state of any form of data. In the market, there are several state management libraries for Angular like [NGRX](https://ngrx.io), [NGXS](https://www.ngxs.io), [Akita](https://datorama.github.io/akita), etc. and all of them have different usages and purposes.

We can choose suitable state management for our application before we implement it.

Some benefits of using state management.

1. It enables sharing data between different components
1. It provides centralized control for state transition
1. The code will be clean and more readable
1. Makes it easy to debug when something goes wrong
1. Dev tools are available for tracing and debugging state management libraries

**[Back to top](#table-of-contents)**

## Use Environment Variables

Angular provides environment configurations to declare variables unique for each environment. The default environments are `development` and `production`. We can even add more environments, or add new variables in existing environment files.

Use it when you depend on different values on different environments.

Development environment (the default).

> environment.ts

```ts
export const environment = {
  production: false,
  baseApiUrl: 'http://localhost:8080',
};
```

Production environment.

> environment.prod.ts

```ts
export const environment = {
  production: true,
  baseApiUrl: 'https://api.example.com',
};
```

**[Back to top](#table-of-contents)**

## Divide Imports

Keeping your file imports ordered and neat is challenging, especially when using an IDE to auto-add them as you type. As your files grow, they tend to get quite messy.

It's good practice dividing the imports by these types:

1. Angular imports always go at the top
1. RxJS imports
1. Third parties (non-core)
1. Local/Project imports at the end

It’s also a good practice to leave a comment above each group, but it's not required unless there is a lot of imports.

```ts
// Angular.
import { ChangeDetectionStrategy, Component } from '@angular/core';

// RxJS.
import { map } from 'rxjs/operators';
import { Observable } from 'rxjs';

// Third Parties.
import { MatDialog } from '@angular/material/dialog';

// Local.
import { AuthFacade } from '@my-project/auth';
```

**[Back to top](#table-of-contents)**

## Prefer Observables Over Promises

[Observables](https://rxjs-dev.firebaseapp.com/guide/observable) partly overlaps the standard JavaScript [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) functionality. Both are meant to handle asynchronous code. However, Observables can do so much more than Promises. Observables can resolve to more than just one value, because they are a stream of values. Observables are everywhere in Angular Framework. We can see that, by looking at the Angular `HttpClient`. It returns Observables, even when it is clear, that a HTTP call can never result in more than one response. Mixing Observables with Promises isn't a good solution. That way, we have completely different implementations, that are hardly compatible with each other in different parts of our application.

**[Back to top](#table-of-contents)**

## Component Properties and Methods Order

* Add public and private properties above the constructor
* Add public and private methods right below the constructor or if you have life cycle hooks so after them
* Locate the `properties` and `methods` with the same decorator close to each other and write empty line in between groups of properties with the same decorator.

```ts
export class MyComponent implements OnInit {
  @Input() value = '';
  @Input() otherValue = '';

  @Output() valueChanged = new EventEmitter<string>();
  @Output() otherValueChanged = new EventEmitter<string>();

  @ViewChild(ChildDirective) child!: ChildDirective;

  @ViewChildren(ChildDirective) viewChildren!: QueryList<ChildDirective>;

  @ContentChild(ChildDirective) contentChild!: ChildDirective;

  @ContentChildren(ChildDirective) contentChildren!: QueryList<ChildDirective>;

  private hiddenValue = '';

  constructor() {}
  
  ngOnInit(): void {}

  @HostBinding('class.valid')
  isValid(): boolean {
    return true;
  }

  @HostListener('click', ['$event'])
  onClick(event): void {}

  myPublicFunc(): void {}
  
  private myPrivateFunc(): void {}
}
```

**[Back to top](#table-of-contents)**

## Lifecycle Hooks Interfaces and Order

Adding lifecycle hooks interfaces is not mandatory but a suggested practice.

Ideally, they should be defined in the same order they execute and after the `constructor`.

```ts
class MyComponent implements OnChanges, OnInit, DoCheck,
  AfterContentInit, AfterContentChecked, AfterViewInit,
  AfterViewChecked, OnDestroy {

  constructor() {}

  ngOnChanges(): void {}

  ngOnInit(): void {}

  ngDoCheck(): void {}

  ngAfterContentInit(): void {}

  ngAfterContentChecked(): void {}

  ngAfterViewInit(): void {}

  ngAfterViewChecked(): void {}

  ngOnDestroy(): void {}	
}
```

**[Back to top](#table-of-contents)**

## Write Logic Outside Lifecycle Hook

Avoid directly writing any logic within the lifecycle hooks, encapsulate logic within private methods and call them within the lifecycle hooks.

```typescript
export class MyComponent implements OnInit {
  ngOnInit(): void {
    this.init();
  }
  
  private init(): void {
   // ...
  }
}
```

**[Back to top](#table-of-contents)**

## Component Event Names Rules

Follow this rules will help you to decide better event names:

* Do not prefix events/outputs names with `on`. The handler, instead, could be written with such prefix
* Always specify the entity whose action referred, not only the action itself.
  If we are describing an event on a component whose **value changed**, the event change could be `valueChange`.
* Use past-sense or not (`valueChange` or `valueChanged`)

**[Back to top](#table-of-contents)**

## HTML Wrapping and Order

Do not exceed 80 characters per column for all files, it’s simply much easier to read vertically than horizontally.

### Rules for Writing HTML Tags

* When an element has two or more attributes, write **one attribute** per line
* Attributes have to be written **in a specific order**
* Unless using a single attribute, the closing tag has to be written **on the next line**
* Add structural directives only to `ng-container` elements

Attributes order:

1. Structural directives (`*ngIf`, `*ngFor`, `*ngSwitch`)
1. Animations (`@myAnimation`)
1. Template variables (`#myElement`)
1. Static properties (`id`, `class`, `aria-label`)
1. Dynamic properties (`[id]`, `[class]`, `[attr.aria-label]`)
1. Events (`(click)`, `(myEvent)`)
1. Two-way binding (`[(value)]`)

**Why?**: This can facilitate reading through and understanding the structure of your templates.

**Before**

```html
<input #myElement (input)="onInputChanged($event)" [(value)]="myModel" *ngIf="canEdit" class="form-control" [attr.placeholder]="placeholder" @fadeIn type="text" />
```

**After**

```html
<ng-container *ngIf="canEdit"> 
  <input
    @fadeIn
    #myElement
    type="text"
    class="form-control"
    [attr.placeholder]="placeholder"
    (input)="onInputChanged($event)"
    [(value)]="myModel"
  />
</ng-container>
```

**[Back to top](#table-of-contents)**

## Wrap Pipes Within Parenthesis

Wrap pipes expressions within parenthesis.

**Why?**: The feeling of division provided by the parenthesis gives a clue that the value is being transformed.

```html
<ng-container *ngIf="(movies$ | async) as movies">
  <!-- ... -->
</ng-container>
```

When using multiple pipes, it may even be more important:

```html
<input 
 [value]="(value$ | async | uppercase | trim)"
/>
```

**[Back to top](#table-of-contents)**

## Avoid Logic in Templates

If you have any sort of logic in your templates, even if it is a simple && clause, it is good to extract it out into its component.

***Why?***: Having logic in the template means that it is not possible to unit test it, and therefore it is more prone to bugs when changing template code.

**Before**

```html
<p *ngIf="role === 'developer'">Status: Developer</p>
```

```ts
@Input() role?: Role;
```

**After**

```html
<p *ngIf="isDeveloper"></p>
```

```ts
@Input role?: Role;

get isDeveloper(): boolean {
  return this.role === 'developer';
}
```

**[Back to top](#table-of-contents)**

## Prevent Memory Leaks

When we navigate from one component to the other component, the first component is destroyed and the other component initializes. The first component was subscribed to the Observable and now the component is destroyed. This can cause memory leaks.

### Use of takeUntil Operator

`takeUntil` is also an operator. It allows monitoring the Observables and get rid of the subscriptions once the value is emitted by Observables. We can conclude that it secures the Observables from getting leaked.

```ts
ngOnInit(): void {
  this.movieService.getListUpdates()
    .pipe(takeUntil(this.ngUnsubscribe))
    .subscribe(movies => {
      this.movies = movies;
    });
}

ngOnDestroy(): void {
  this.ngUnsubscribe.next();
  this.ngUnsubscribe.complete();
}
```

### Use of async Pipe

It subscribes to an Observable or Promise and returns to the recent emitted value and unsubscribe when the component is destroyed.

```html
<ul *ngIf="(movieService.getListUpdates() | async) as movies">
  <li *ngFor="let movie of movies">
    {{ movie.title }}
  </li>
</ul>
```

### Use of take(1)

It takes the value and allows for not subscribing whenever a new value is diagnosed. It takes care that you receive data only once.

```ts
  this.movieService.getList()
    .pipe(take(1))
    .subscribe(movies => {
      this.movies = movies;
    });
```

**[Back to top](#table-of-contents)**

## Subscribe in Template Using async Pipe

Avoid subscribing to observables from components and instead subscribe to the observables from the template.

***Why?***: `async` pipe unsubscribe automatically, and it makes the code simpler by eliminating the need to manually manage subscriptions. It also reduces the risk of accidentally forgetting to unsubscribe a subscription in the component, which would cause a memory leak. This risk can also be mitigated by using a lint rule to detect unsubscribed observables.

**Before**

```html
<p>{{ textToDisplay }}</p>
```

```ts
textToDisplay = '';

ngOnInit(): void {
  this.textSubscriotion = this.textService
    .pipe(
      map(value => value.item),
    )
    .subscribe(item => this.textToDisplay = item);
}

ngOnDestroy(): void {
  if (this.textSubscriotion) {
    this.textSubscriotion.unsubscribe();
  }
}
```

**After**

```html
<p>{{ (textToDisplay$ | async) }}</p>
```

```ts
textToDisplay$ = this.textService.pipe(map(value => value.item));
```

**[Back to top](#table-of-contents)**

## Use Change Detection OnPush

Use the `OnPush` change detection strategy to tell Angular there have been no changes. This lets you skip the entire change detection step.
This change detection works by detecting if some new data has been explicitly pushed into the component, either via a component input or an Observable subscribed to using the async pipe.

***Why?***: The more use of `OnPush` in components we have the fewer checks Angular needs to perform, means better performance.

```html
<app-todo *ngFor="let todo of todos" [todo]="todo"></app-todo>
```

```ts
@Component({
  selector: 'app-todo-list',
  templateUrl: './todo-list.component.html',
  styleUrls: ['./todo-list.component.scss'],
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class TodoListComponent {
  @Input() todos;
}
```

**[Back to top](#table-of-contents)**

## Avoid Having Subscriptions Inside Subscriptions

Sometimes you may want values from more than one observable to perform an action. In this case, avoid subscribing to one observable in to subscribe block of another observable. Instead, use appropriate chaining operators. Chaining operators run on observables from the operator before them. Some chaining operators are: `withLatestFrom`, `combineLatest`, etc.

**Before**

```ts
firstObservable$.pipe(
    take(1)
  )
  .subscribe(firstValue => {
    secondObservable$.pipe(
        take(1)
      )
      .subscribe(secondValue => {
        console.log(`Combined values are: ${firstValue} & ${secondValue}`);
      });
  });
```

**After**

```ts
firstObservable$.pipe(
    withLatestFrom(secondObservable$),
    first()
  )
  .subscribe(([firstValue, secondValue]) => {
      console.log(`Combined values are: ${firstValue} & ${secondValue}`);
  });
```

**[Back to top](#table-of-contents)**

## Use trackBy Along With ngFor

When using `ngFor` to loop over an array in templates, use it with a `trackBy` function which will return a unique identifier for each item.

***Why?***: When an array changes, Angular re-renders the whole DOM tree. But if you use trackBy, Angular will know which element has changed and will only make DOM changes for that particular element.

**Before**

```html
<li *ngFor="let movie of movies">{{ movie.title }}</li>
```

**After**

```html
<li *ngFor="let movie of movies; trackBy: trackByFn">{{ movie.title }}</li>
```

```ts
trackByFn(index, movie: Movie): string {
  return movie.id;
}
```

**[Back to top](#table-of-contents)**

## Strings Should Be Safe

If you have a variable of type string that can have only a set of values, instead of declaring it as a string type, you can declare the list of possible values as the type.

***Why?***: By declaring the type of the variable appropriately, we can avoid bugs while writing the code during compile time rather than during runtime.

```ts
export class ButtonComponent {
  @Input() type: string;
}
```

```ts
export class ButtonComponent {
  @Input() type: 'submit' | 'reset' | 'button' = 'button';
}
```

**[Back to top](#table-of-contents)**

## Avoid any Type

Declare variables or constants with proper types other than any.

***Wny?***: This will reduce unintended problems. Another advantage of having good typings in our application is that it makes refactoring easier.

**Before**

```ts
export class MovieComponent {
  movie: any;
  
  constructor() {
    this.movie = {
      // Whatever we want can be decaler here...
    };
  }
}
```

**After**

```ts
interface Movie {
  title: string;
}

export class MovieComponent {
  movie: Movie;

  constructor() {
    this.movie = {
      title: 'Avengers',
      // We can't decalre other properties...
    };
  }
}
```

**[Back to top](#table-of-contents)**

## Use Mandatory Inputs

To make the requirement explicit we can use the selector in the `@Component` decorator to require that the attribute on our component must exist.

```ts
@Component({
  selector: 'movie-list[movies]',
})
export class MovieListComponent {
  @Input() movies: Movies[];
}
```

Resulting an error, when we start the application or at compile time when the application is built Ahead of Time (AoT), if the `MovieListComponent` doesn't have an items attribute. This approach improves the readability of the code because helps other developers to integrate this component into their projects, throwing errors, and we don't need to define explicit validations to check if it exists.

**[Back to top](#table-of-contents)**

## Do Not Pass Streams to Components Directly

Passing streams to child components is a bad practice because it creates a very close link between the parent component and the child component. A component should always receive an object or value and should not even care if that object or value comes from a stream or not. It is better to handle the subscription in the parent component itself. Angular has a feature called the `async` pipe that can be used for this.

**[Back to top](#table-of-contents)**

## Do Not Pass Streams to Services

By passing a stream to a service we don't know what's going to happen to it. The stream could be subscribed to, or even combined with another stream that has a longer lifecycle, that could eventually determine the state of our application. Subscriptions might trigger unwanted behavior. It's recommended to use higher order streams in the components for these situations.

**[Back to top](#table-of-contents)**

## Do Not Expose Subjects

In order to avoid side effects to subject value it's better to hide the subject itself in the service and to expose the observable of the subject and function update his values.

```ts
export class CartService {
  private selectedItem: BehaviorSubject<CartItem | null> = new BehaviorSubject<CartItem | null>(null);

  readonly selectedItem$: Observable<CartItem | null> = this.selectedItem.asObservable();

  updateSelectedItem(item: CartItem): void {
    this.selectedItem.next(item);
  }
}
```

**[Back to top](#table-of-contents)**

## Handle RxJS Errors

Error handling is an essential part of RxJS. By default, if something goes wrong with an Observable, it just dies. If we don't deal with such errors, it will happen silently, and we won't know why we are not receiving data anymore.

**[Back to top](#table-of-contents)**

## Avoid Changing the DOM Directly

It's important to know that Angular uses Lifecycle Hooks that determine how and when components will be rendered and updated. Direct DOM access or manipulation can corrupt these lifecycle hooks, leading to unexpected behavior of the whole app. Direct access to the DOM can make our application more vulnerable to `XSS attacks`. Use `ElementRef` as the last resort when direct access to DOM is needed. Use templating and data-binding provided by Angular instead. Alternatively we can take a look at `Renderer2` which provides API that can safely be used even when direct access to native elements is not supported.

**[Back to top](#table-of-contents)**

## Avoid Computing Values in the Template

Sometimes in Angular templates, we may be tempted to bind a method in the HTML template. The problem is that the methods are constantly getting called during the Angular Change Detection Cycle.

```html
<h1>{{ getTitle() }}</h1>
```

```ts
export class HomeComponent {
  getTitle(): string {
    return 'Home Page';
  }
}
```

It's highly recommended not to use methods calls in Angular template expressions. While method calls in Angular templates are super convenient and technically valid, they may cause serious performance issues because the method is called every time change detection runs. Instead, we can use pure `pipes` or manually calculate the values with `Lifecycle Hooks`.

**[Back to top](#table-of-contents)**

## Use Immutability

Objects and arrays are the reference types in javascript. If we want to copy them into another object or an array and to modify them, the best practice is to do that in an immutable way using spread operator `…` this will prevent from changing the original object or array.

In Angular, it's very critical since we can modify the original array or object in the service or component and get unexpected behavior.

```ts
// Somewhere in the code we have list of movies...
const movies = [
  {
    title: 'Avengers',
    year: 2012
  },
];

// And in other place we get the movies list...
const updatedMovies = [...movies]; // Update with spread operator...
```

Please notice that using spread operator is copy only one level! you need to use spread operator to each level or instead to use deep cloning like this:

```ts
const updatedMovies = JSON.parse(JSON.stringify(movies));
```

**[Back to top](#table-of-contents)**

## Safe Navigation Operator in HTML Template

To be on the safe side we should use the safe navigation operator while accessing a property from an object in a component’s template. If the object is null, and we try to access a property, we are going to get an exception. But if we use the save navigation `(?)` operator, the template will ignore the null value and will access the property once the object is not the null anymore.

```html
<ng-container *ngif="movie">
  <p>{{ movie.details.description }}</p>
</ng-container>
```

**[Back to top](#table-of-contents)**

## Break Down Into Small Reusable Components

This might be an extension of the Single responsibility principle. Large components are very difficult to debug, manage and test. If the component becomes large, break it down into more reusable smaller components to reduce duplication of the code, so that we can easily manage, maintain and debug with less effort.

```text
--ParentComponent
----TitleComponent
----BodyComponent
----ListComponent
------ItemComponent
----FooterComponent
```

**[Back to top](#table-of-contents)**

## Use Smart and Dumb Components

This pattern helps to use `OnPush` change detection strategy to tell Angular there have been no changes in the dumb components.

`Smart components` are used in manipulating data, calling the APIs, focussing more on functionalities, and managing states. While `dumb components` are all about cosmetics, they focus more on how they look.

**[Back to top](#table-of-contents)**

## Use Lazy Loading

When possible, try to lazy load the modules in your Angular application. Lazy loading is when you load something only when it is used, for example, loading a component only when it is to be seen.

***Why?***: This will reduce the size of the application to be loaded and can improve the application boot time by not loading the modules that are not used.

**Before**

```ts
const routes: Routes = [
  {
    path: '',
    pathMatch: 'full',
    component: HomeComponent,
  },
];
```

**After**

```ts
const routes: Routes = [
  {
    path: '',
    pathMatch: 'full',
    loadChildren: () => import('./features/home/home.module').then(m => m.HomeModule),
  },
];
```

**[Back to top](#table-of-contents)**

## Use index.ts

Instead of remembering multiple source file names, there are some tiny import statements that will fulfill the purpose.

***Why?***: It helps to keep all correlated files in a single location.

**Before**

```ts
import { uuid } from './../utils/uuid';
import { convertToTitleCase } from './../utils/convert-to-title-case';
```

**After**

> utils/index.ts

```ts
export * from './uuid';
export * from './convert-to-title-case';
```

Now we can import all the files from one file.

```ts
import { uuid, convertToTitleCase } from './../utils';
```

**[Back to top](#table-of-contents)**

## Isolate API Hacks

Sometimes, we need to add some logic in the code to make up for bugs in the APIs. Instead of having the hacks in components where they are needed, it is better to isolate them in one place like in a function or a service and use them. When fixing the bugs in the APIs, it is easier to look for them in one file rather than looking for the hacks that could be spread across the codebase.

**[Back to top](#table-of-contents)**

## Cache API Calls

Caching API calls improves performance and saves memory by limiting server requests to fetch redundant information. Some API responses may not change frequently so we can put some caching mechanism and can store those values from the API. When the same API request is made, we can get a response from the cache. Thus, it speeds up the application and also makes sure that we are not downloading the same information frequently.

You can use for example RxJS `shareReplay` operator.

```ts
class MoviesService {
  private commonMovies$: Observable<Movie[]> | null = null;

  
  getCommonMovies(): Observable<Movie[]> {
    if (!this.commonMovies$) {
      this.commonMovies$ = this.http.get<Movie[]>('/api/movies/common').pipe(
        shareReplay(1)
      );
    }
    return this.commonMovies$;
  }
}
```

**[Back to top](#table-of-contents)**

## Use CDK Virtual Scroll

CDK (Component Development Kit) Virtual Scroll can be used to display large lists of elements more efficiently. Virtual scrolling enables an efficient way to simulate all values by making the height of the container element equal to the height of the total number of elements.

For more info: [Angular material cdk virtual scroll](https://material.angular.io/cdk/scrolling/overview)

**[Back to top](#table-of-contents)**

## Use Angular Service Workers and PWA

Angular service worker is designed to optimize the end user experience of using an application over a slow or unreliable network connection, while also minimizing the risks of serving outdated content.

For more info: [How to use Angular service worker and pwa](https://angular.io/guide/service-worker-getting-started)

**[Back to top](#table-of-contents)**

## Use Angular Universal

A normal Angular application executes in the browser, rendering pages in the DOM in response to user actions. Angular Universal executes on the server, generating static application pages that later get bootstrapped on the client. This means that the application generally renders more quickly, giving users a chance to view the application layout before it becomes fully interactive.

For more info: [Server-side rendering (SSR) with Angular Universal](https://angular.io/guide/universal)

## Use Lint Rules

[ESLint](https://github.com/eslint/eslint) and [Stylelint](https://github.com/stylelint/stylelint) have various inbuilt options, it forces the program to be cleaner and more consistent. It is widely supported across all modern editors and can be customized with your own lint rules and configurations. This will ensure consistency and readability of the code.

**[Back to top](#table-of-contents)**

# License

[MIT](LICENSE)
