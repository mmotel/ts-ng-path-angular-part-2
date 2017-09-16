# Serwisy

Poza modułami oraz komponentami bardzo istotną częścią aplikacji są serwisy. 

![](/assets/app logic spliting.png)

Są one odpowiedzialne między innymi za powtarzającą się logikę, komunikację z serwerem czy też obsługę komunikacji wewnątrz aplikacji.

### podstawy

Serwis to klasa opatrzona dekoratorem `@Injectable`.

```js
@Injectable()
export class SomeService {}
```

`@Injectable` oznacza klasę jako możliwą do wstrzyknięcia przez framework do zarządzania zależnościami.

` - - - `

Zbudujemy serwis obsługujący [`localStorage`](https://developer.mozilla.org/pl/docs/Web/API/Window/localStorage). 

Przykład: [local-storage.service.ts](https://github.com/mmotel/ng-beers-app/blob/v11/src/app/shared/service/local-storage/local-storage.service.ts) `v11`.

### dostarczanie serwisów

Aby móc wykorzystać serwis w komponencie musimy go dostarczyć. Robimy to poprzez umieszczenie serwisu w tablicy `providers`. Mamy do wyboru dostarczenie serwisu w module lub komponencie. 

Zalecaną praktyką jest dostarczanie serwisów na poziomie modułów. Głównie ze względu na, to że podczas importowania modułu zyskujemy również dostęp do dostarczanych serwisów.

Jest jedna sytuacja, w której dostarczanie serwisów w module nie jest idealnym rozwiązaniem. Gdy serwis przechowuje stan mocno powiązany z komponentem - na przykład sesję czatu. Dostarczenie serwisu w komponencie pozwoli za każdym razem otrzymać jego nową instancję - na przykład gdy otwieramy kolejne okienko rozmowy.

```ts
@NgModule({
  //...
  providers: [
    LocalStorageService
  ],
  //...
})
export class AppModule {}
```

Po dostarczeniu serwisu w aplikacji, kolejnym krokiem jest jego wstrzyknięcie do komponentu lub innego serwisu.  

```ts
  constructor (
    private _localStorage: LocalStorageService
  ) { }
```

Przykłady: [app.module.ts](https://github.com/mmotel/ng-beers-app/blob/v15/src/app/app.module.ts), [favourite-beers.service.ts](https://github.com/mmotel/ng-beers-app/blob/v15/src/app/favourite/service/favourite-beer/favourite-beer.service.ts) `v15`

`- - -`

Obecnie część serwisów w naszej aplikacji jest dostarczana w komponentach. Przyjrzyjmy się im i poprawny miejsce ich dostarczenia zgodnie z wyżej wymienionymi zaleceniami.

Aplikacja po zmianach `v24` ([github](https://github.com/mmotel/ng-beers-app/tree/v24/src/app)).

### `cache`

![](/assets/service cahce.png)

W przypadku niektórych danych warto byłoby je zapamiętać po pierwszym pobraniu. Idealnymi kandydatami są dane, które są często potrzebne a zmieniają się relatywnie rzadko, na przykład profil użytkownika czy ustawienia aplikacji.

Kiedy nasz serwis pełni również funkcję `cache`-a należy zwrócić uwagę gdzie go dostarczamy. Najlepszym miejsce na to jest oczywiście moduł, a dokładniej `AppModule`.

`- - -`

W naszej aplikacji warto byłoby zapamiętać listę piw, której pobranie jest najbardziej kosztowne.

Przykład: [beers.service.ts](https://github.com/mmotel/ng-beers-app/blob/v25/src/app/shared/service/beer.service.ts) `v25`


---

###### Źródła

* https://angular.io/tutorial/toh-pt4#create-the-heroservice