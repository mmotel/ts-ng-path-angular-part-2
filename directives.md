# Dyrektywy

`Angular` ma trzy rodzaje dyrektyw:

* **komponenty** - dyrektywy z szablonem,

* **dyrektywy strukturalne** - zmieniają układ `DOM`-u dodając oraz usuwając jego elementy, na przykład `*ngFor`, `*ngIf`,

* **dyrektywy atrybutu** - zmieniają wygląd oraz zachowanie elementów `DOM`, komponentów czy też innych dyrektyw.


## Dyrektywy atrybutu

Dyrektywa atrybutu (_ang. attribute directive_) pozwala uzyskać dostęp do natywnego elementu `DOM`-u i dokonać jego modyfikacji.

Najpopularniejszą dyrektywą atrybytu jest [`ngStyle`](https://angular.io/api/common/NgStyle), która służy do manipulacji stylami elementu.

```html
<div [ngStyle]="{'style-name': styleValue}">
 <!-- ... -->
</div>
```

### podstawy

Dyrektywy podobnie jak komponenty mają swoje selektory. Definiujemy je podając metadane do dekoratora `@Directive`. 

**Ważnym szczegółem jest konieczność otoczenia nazwy dyrektywy kwadratowymi nawiasami `[]` aby mógł on być używany jako atrybut.**

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

### cykl życia

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

### dodatkowe parametry

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

### wykorzystanie

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

Dyrektywy strukturalne (_ang. structural directive_) służą do manipulowania układem elementów widoku. Zazwyczaj poprzez dodawanie, usuwanie oraz modyfikowanie elementów `DOM`. 

Najpopularniejszymi przykładami są `*ngIf` oraz `*ngFor`. 

### przedrostek `*`

Dyrektywę strukturalną łatwo rozpoznać dzięki przedrostkowi `*`. Nie jest to jednak jedynie konwencja ale uproszczona notacja, którą `Angular` tłumaczy na element `<ng-template>`.

### `*ngIf`

Aby zobaczyć co dzieje się _pod maską_ przyjrzymy się bliżej dyrektywie `*ngIf`.

```html
<div *ngIf="condition">
    <!-- ... -->
</div>
```

Gdy kompilator widzi taki zapis zamienia go na atrybut `tempate`.

```html
<div template="ngIf condition">
    <!-- ... -->
</div>
```

Kolejnym krokiem jest zamiana na `<ng-tempalte>` z prostym przypisaniem atrybutu `[ngIf]`.

```html
<ng-template [ngIf]="conditin">
    <div>
        <!-- ... -->
    </div>
</ng-template>
```

W tym momencie `*ngIf` ma już proste zadanie i działa dokładnie tak jak dyrektywa atrybutu, która umieszcza bądź usuwa swoją zawartość w elemencie `<ng-tempalte>`.

Aby móc dokonać tej manipulacji potrzebujemy dostp do elementów reprezentujących:

 * zawartość szablonu - [`TemplateRef`](https://angular.io/api/core/TemplateRef),
 * miejsce, w którym został on zdefiniowany - [`ViewContainerRef`](https://angular.io/api/core/ViewContainerRef).
 
Implementacja `*ngIf` może wyglądać następująco:

```ts
@Directive({
  selector: '[ngIf]'
})
export class NgIfDirective {

  @Input() set ngIf (condition: boolean) {
    if (condition) {
      this.viewContainer.createEmbeddedView(this.templateRef);
    } else {
      this.viewContainer.clear();
    }
  }

  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) {}

}
```



#### Dla zainteresowanych: [Nir Kaufman - Demystified Angular Directives (JS-Poland 2017)](https://youtu.be/bVyw2njDoZw?t=1m10s)

---

###### Źródła

* https://angular.io/guide/attribute-directives
* https://angular.io/guide/structural-directives