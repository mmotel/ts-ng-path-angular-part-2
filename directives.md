# Dyrektywy

## Atribute directive

```js
@Directive({ selector: '[myHighlight]' })
export class HighlightDirective {
    constructor(el: ElementRef) {
       el.nativeElement.style.backgroundColor = 'yellow';
    }
}
```

## Structural directive

### *ngIf

### *ngFor