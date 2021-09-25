# Angular Best Practices

[![Angular](assets/angular.png)](https://angular.io)

Angular guide for teams that look for consistency through best practices.

## Table of Contents

1. [Use trackBy along with ngFor](#use-trackby-along-with-ngfor)
1. [Use Lazy Loading](#use-lazy-loading)

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

# License

[MIT](LICENSE)
