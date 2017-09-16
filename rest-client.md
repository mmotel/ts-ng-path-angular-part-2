# Klient REST API

Wraz z rozwojem aplikacji rośnie ilość serwisów, które korzystają z API. Wszystkie one muszą zajmować się autoryzacją czy też parsowaniem odpowiedzi serwera.

![](/assets/services to api.png)

Znacznie lepszym rozwiązaniem jest stworzenie serwisu, który będzie adapterem/fasadą ukrywającą powtarzalne elementy komunikacji z API. Zajmie się on autoryzacją, obsługą typowych błędów - `404`, `500` - czy też wyciąganiem z odpowiedzi interesujących nas danych.

![](/assets/services to rest client to api.png)

`- - -`

W naszej aplikacji obecnie z API korzysta jeden serwis. Pomimo tego część implementacji metod się powtarza. Stworzymy swój  `RestClientService`, w którym ukryjemy część implementacji.

Przykłady: [beer.service.ts](https://github.com/mmotel/ng-beers-app/blob/v26/src/app/shared/service/beer.service.ts), [rest-client.service.ts](https://github.com/mmotel/ng-beers-app/blob/v26/src/app/shared/service/rest-client/rest-client.service.ts) `v26`