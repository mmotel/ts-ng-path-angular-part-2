# Dyrektywy

`Angular` ma trzy rodzaje dyrektyw:

* **komponenty** - dyrektywy z szablonem,

* **dyrektywy strukturalne** - zmieniają układ `DOM`-u dodając oraz usuwając jego elementy, na przykład `*ngFor`, `*ngIf`,

* **dyrektywy atrybutu** - zmieniają wygląd oraz zachowanie elementów `DOM`, komponentów czy też innych dyrektyw.


## Dyrektywy atrybutu

Dyrektywa atrybutu (_ang. attribute directive_) pozwala uzyskać dostęp do natywnego elementu `DOM`-u i dokonać jego modyfikacji.

Dyrektywy podobnie jak komponenty mają swoje selektory. Definiujemy je podając metadane do dekoratora `@Directive`. 

```ts
@Directive({ 
    selector: '[appAutoFocus]' 
})
export class AutoFocusDirective {}
```

Dostęp do elementu uzyskujemy w konstruktorze, który jako parametr otrzymuje obiekty typu `ElementRef`.

```ts
@Directive({ 
    selector: '[appAutoFocus]' 
})
export class AutoFocusDirective {

    constructor(element: ElementRef) {
        //...
    }

}
```

W dyrektywie podobnie jak w komponencie możemy skorzystać z [uchwytów do jego cyklu życia](https://mmotel.gitbooks.io/ts-ng-path-angular-part-1/content/component-lifecycle.html). Aby to zrobić poprostu je implementujemy.

```ts
@Directive({ 
    selector: '[appAutoFocus]' 
})
export class AutoFocusDirective implements AfterViewInit {

    constructor(element: ElementRef) {
        //...
    }
    
    ngAfrterViewInit () {
        //...
    }

}
```

Mamy również możliwość definiowania dodatkowych parametrów dyrektyw. Ponownie, podobnie jak w komponentach, korzystamy z `@Input`.

```ts
@Directive({ 
    selector: '[appAutoFocus]' 
})
export class AutoFocusDirective implements AfterViewInit {

    @Input('appAutoFocusActive') isActive: boolean;

    constructor(element: ElementRef) {
        //...
    }
    
    ngAfrterViewInit () {
        //...
    }

}
```

Aby wykorzystać naszą dyrektywę umieszczamy ją w wybranym elemencie szablonu.

```html
<md-input-container>
  <input mdInput
    [(ngModel)]="searchPhrase"
    [disabled]="!isActive"
    appAutoFocus
    [appAutoFocusActive]="isActive"
    type="text"
    placeholder="Search..."
  >
</md-input-container>
```

`- - -`

Zbudujemy swoją dyrektywę, która będzie ustawiała `focus` na naszą wyszukiwarkę piw kiedy stanie się ona aktywna.

Przykłady: [beers-search.component.html](https://github.com/mmotel/ng-beers-app/blob/v28/src/app/shared/beers-search/beers-search.component.html), [auto-focus.directive.ts](https://github.com/mmotel/ng-beers-app/blob/v28/src/app/shared/directive/auto-focus.directive.ts) `v28`

## Dyrektywy strukturalne

### `*ngIf`

### `*ngFor`


---

###### Źródła

* https://angular.io/guide/attribute-directives
* https://angular.io/guide/structural-directives