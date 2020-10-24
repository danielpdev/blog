---
title: "Angular directive basics [2] - Adding styles"
date: "2018-06-20"
cover: './preview.png'
tags: ['markdown', 'angular', 'directives']
---

## Directive with styles

There are time when you want to build a directive but you also require to add some minor CSS styles for it, unfortunately this is not possible with the current implementation of [@Directive in Angular.](https://angular.io/api/core/Directive)

But there is a chance to do just that by adding into play the [@Component decorator.](https://angular.io/api/core/Component)

### How should work?

Suppose we have a directive like this:

import {Directive} from '@angular/core';
```js
@Directive({
  selector: 'my-directive',
})
export class MyDirective {
}
```

The next step will be to bring the @Component decorator and add some styles for our background color.
```js
import {Directive, Component} from '@angular/core';
@Component({ 
  selector: '[my-directive]', 
  template: '<ng-content></ng-content>',
  styles: [`
    :host {
      color:red;
    }
  `] 
}) 
@Directive({ 
  selector: '[my-directive]'
  })
export class MyDirective { 
}
```

You see how we set the template to `template: '<ng-content></ng-content>'` because we want any content that will reside in our component to be available.

At this point we can remove the @Directive decorator because we don't really need it anymore as we don't have a directive anymore but a brand new component which acts as a directive.

HTML
```html
<p my-directive>
  Font color should be red
</p>
```
 

Hope this helps. New articles on directives and angular tips coming soon. Enjoy.
