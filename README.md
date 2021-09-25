# Angular Best Practices

[![Angular](assets/angular.png)](https://angular.io)

Angular guide for teams that look for consistency through best practices.

## Table of Contents

1. [trackBy](#trackby)

## trackBy

- When using `ngFor` to loop over an array in templates, use it with a 
  `trackBy` function which will return a unique identifier for each item.

*Why?*: When an array changes, Angular re-renders the whole DOM tree. But if you use trackBy, Angular will know which element has changed and will only make DOM changes for that particular element.

**Before**

```html
<li *ngFor="let item of items;">{{ item }}</li>
```

**After**

```html
<li *ngFor="let item of items; trackBy: trackByFn">{{ item }}</li>
```

```ts
trackByFn(index, item): string {    
   return item.id;
}
```

**[Back to top](#table-of-contents)**

# License

[MIT](LICENSE)
