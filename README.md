# Angular Best Practices

[![Angular](assets/angular.png)](https://angular.io)

Angular guide for teams that look for consistency through best practices.

## Table of Contents

1. [Avoid Logic in Templates](#avoid-logic-in-templates)
1. [Subscribe in Template Using Async Pipe](#subscribe-in-template-using-async-pipe)
1. [Avoid Having Subscriptions Inside Subscriptions](#avoid-having-subscriptions-inside-subscriptions)
1. [Use trackBy along with ngFor](#use-trackby-along-with-ngfor)
1. [Strings Should Be Safe](#strings-should-be-safe)
1. [Use Lazy Loading](#use-lazy-loading)
1. [Use index.ts](#use-index.ts)

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

## Subscribe in Template Using Async Pipe

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
<p>{{ textToDisplay$ | async }}</p>
```

```ts
textToDisplay$ = this.textService.pipe(map(value => value.item));
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

## Use trackBy along with ngFor

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

# License

[MIT](LICENSE)
