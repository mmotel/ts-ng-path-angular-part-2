# Potoki

Każda aplikacja ma w zasadzie to samo proste zadanie - pobrać i wyświetlić dane. W toku prac zauważamy, że dokonujemy często tych samych transformacji pewnych danych. Idealnym rozwiązaniem byłoby dodawanie tych transformacji w `HTML`-u podobnie jak dodajemy style.

Z pomocą przychodzą nam potoki (_ang. pipes_). 

![](/assets/pipe.png)

### podstawy

Aby skorzystać z potoku używamy notacji jaką możemy znać między innymi z systemu `Linux`. 

```ts
{{ beer.name | uppercase }}
```

Dodatkowe parametry potoku umieszczamy po znaku `:`.

```ts
{{ beer.name | slice: 10 }}

```

Możemy również łączyć ze sobą potoki.

```ts
{{ beer.name | slice: 10 | uppercase }}

```

### wbudowane potoki

`Angular` ma zbiór wbudowanych potoków dostępnych w każdym szablonie.

Oto kilka z nich:

* [`DatePipe`](https://angular.io/api/common/DatePipe),
* [`JsonPipe`](https://angular.io/api/common/JsonPipe),
* [`CurrencyPipe`](https://angular.io/api/common/CurrencyPipe),
* [`DecimalPipe`](https://angular.io/api/common/DecimalPipe),
* [`PercentPipe`](https://angular.io/api/common/PercentPipe),
* [`SlicePipe`](https://angular.io/api/common/SlicePipe),
* [`LowerCasePipe`](https://angular.io/api/common/LowerCasePipe),
* [`UpperCasePipe`](https://angular.io/api/common/UpperCasePipe),
* [`TitleCasePipe`](https://angular.io/api/common/TitleCasePipe).

## Tworzenie potoków

Oczywiście mamy również możliwość tworzenia swoich własnych potoków. 

Potok jest to klasa posiadająca dekorator `@Pipe()`, do którego przekazujemy jego metadane - najważniejsza jest nazwa.

```ts
@Pipe({name: 'cutWords'})
export class CutWordsPipe {}
```

Drugą istotną kwestią jest implementacja interfejsu [`PipeTransform`](https://angular.io/api/core/PipeTransform).

```ts
export class CutWordsPipe implements PipeTransform {

  transform(value: string, length: number): string {
    // ...
    return value;
  }
  
}
```

`- - -`

Zdefiniujemy potok służący do przycinania napisów do wskazanej długości ale bez _rozcinania_ słów. Następnie wykorzystamy go na widoku listy piw do przycinania opisów do maksymalnie 80 znaków.

Przykłady: [cut-words.pipe.ts](https://github.com/mmotel/ng-beers-app/blob/v27/src/app/shared/pipe/cut-words/cut-words.pipe.ts), [shared/beers-list.component.html](https://github.com/mmotel/ng-beers-app/blob/v27/src/app/shared/beers-list/beers-list.component.html) `v27`


---

###### Źródła

* https://angular.io/guide/pipes