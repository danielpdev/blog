---
title: "Angular directive basics"
date: "2018-06-20"
cover: './preview.png'
tags: ['markdown', 'angular', 'directives']
---

## Angular Directives basics

Angular directives allow you to attach new behavior to DOM elements by using metadata properties:

**Metadata Properties:**

- **exportAs** - actual name that is used by other components inside their templates.
- **host** - js object of class property to host element properties
- **inputs** - list of properties used as inputs
- **outputs** - list of properties used as outputs that others can subscribe to
- **providers** - providers available to this component and its children
- **queries** - configure queries that can be injected into the component
- **selector** - css selector used as indentifier for this component

### Why should you use them?

Whenever you need to add personalized behavior to an element.

For example:

We need to create a component that will be attached
```js
@Directive({
  selector: "[hover]",
  host: {
    "(mouseover)": "onHover($event.target)"
  }
})
export class HoverDirective {
  onHover(btn) {
    console.log(btn);
  }
}
```

We just created a directive that can be used by adding selector `hover` to any element.

### How to use it?

<h1 hover>

</h1>

That's it, you just need to add the selector that was used when the directive was created. Magic happens when we hover over that element and our super onHover methods is invoked.

### Let's use more properties:
```js
@Directive({
  selector: "[hover-with-color]",
  host: {
    "(mouseover)": "onHover($event.target)"
  },
  inputs: ["color"],
  outputs: ["colorChanged"]
})
export class HoverWithColorDirective {
  color: string;
  colorChanged: EventEmitter<string> = new EventEmitter<string>();
  constructor(private el: ElementRef, private renderer: Renderer2) {}
  onHover(element: any) {
    if (element.style.color === this.color) {
      this.renderer.setStyle(element, "color", "#000");
    } else {
      this.renderer.setStyle(element, "color", this.color);
    }
    this.colorChanged.emit(element.style.color);
  }
}
```

In the above example we defined metadata properties for input and output. Using this properties we are able to receive and emit values based on some events that occur when we hover over our element.

### How to use it?
```html

<h1 hover-with-color color="rgb(255, 255, 255)"
   (colorChanged)="onColorChanged($event)">
Hello
</h1>
```

[Read more from official docs.](https://angular.io/api/core/Directive)

Our working examples are here:

<iframe style="width: 100%; height: 500px; border: 0; border-radius: 4px; overflow: hidden;" src="https://codesandbox.io/embed/61wx7057zz?module=%2Fsrc%2Fapp%2Fapp.component.ts" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

