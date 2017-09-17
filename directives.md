# Dyrektywy

`Angular` ma trzy rodzaje dyrektyw:

* **komponenty** - dyrektywy z szablonem,

* **dyrektywy strukturalne** - zmieniają układ `DOM`-u dodając oraz usuwając jego elementy, na przykład `*ngFor`, `*ngIf`,

* **dyrektywy atrybutowe** - zmieniają wygląd oraz zachowanie elementów `DOM`, komponentów czy też innych dyrektyw.

## Dyrektywy atrybutowe

```js
@Directive({ selector: '[myHighlight]' })
export class HighlightDirective {
    constructor(el: ElementRef) {
       el.nativeElement.style.backgroundColor = 'yellow';
    }
}
```

## Dyrektywy strukturalne

### `*ngIf`

### `*ngFor`


---

###### Źródła

* https://angular.io/guide/attribute-directives
* https://angular.io/guide/structural-directives