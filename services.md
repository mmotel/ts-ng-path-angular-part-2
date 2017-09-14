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



### `cache`

---

###### Źródła

* https://angular.io/tutorial/toh-pt4#create-the-heroservice