# Serwisy

Poza modułami oraz komponentami bardzo istotną częścią aplikacji są serwisy. 

![](/assets/app logic spliting.png)

Są one odpowiedzialne między innymi za powtarzającą logikę, komunikację z serwerem czy też obsługę komunikacji wewnątrz aplikacji.

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

### `cache`

---

###### Źródła

* https://angular.io/tutorial/toh-pt4#create-the-heroservice