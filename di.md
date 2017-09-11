# Drzewo zależności

Angular ma własny framework, który zarządza wstrzykiwaniem zależności (_ang. dependency injection_). 

Jego kluczowym elementem są tablice `providers`, które możemy umieścić w metadanych komponentów oraz modułów.

Tworzą one drzewiastą strukturę definiowaną poprzez nawigację oraz zagnieżdżenia komponentów.

![](/assets/injectors tree.png)

Angular poszukując potrzebnej zależności przechodzi od miejsca, w którym jej zażądano w górę aż do momentu kiedy napotka pierwszą tablicę `providers`, która jej dostarcza. 

### Komponent a moduł

Istnieje pewna różnica pomiędzy dostarczaniem zależności w komponentach oraz modułach. 

Te dostarczane w komponencie są tworzone bezpośrednio na jego poziomie.

Natomiast te dostarczane w module są dostarczane na najwyższym poziomie (_root_) i są dostępne w całej aplikacji. 

![](/assets/modules and root injector.png)

Szczególną uwagę na to zachowanie należy zwrócić w przypadku modułów ładowanych leniwie (_ang. lazy loading_). Dostarczone w nich zależności są dostępne w innych modułach dopiero po ich załadowaniu, które może nigdy nie nastąpić.

#### Zalecaną praktyką dostarczania zależności dla całej aplikacji jest dostarczanie ich w `AppModule`.

---

###### Źródła

* https://angular.io/guide/dependency-injection
* https://angular.io/guide/hierarchical-dependency-injection