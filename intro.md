# Wprowadzenie

Omawiany będzie [`Angular`](https://angular.io/docs) w wersji `4.3.5`. 

Wykorzystana została również biblioteka [`Angular Material`](https://material.angular.io) w wersji `2.0.0-beta.8`.

## Wymagania

* [`Node.js`](https://nodejs.org/en/download/) w wersji `6.10` lub nowszej,
* [`npm`](https://www.npmjs.com) w wersji `3.10` lub nowszej (instaluje się wraz z `Node.js`),
* [`Angular CLI`](https://cli.angular.io) w wersji `1.3.1` lub nowszej,

```sh
npm install -g @angular/cli@1.3.1
```

* ulubiony edytor (na przykład [Visual Studio Code](https://code.visualstudio.com)).

## Repozytorium

Kod aplikacja, którą będziemy rozwijać oraz omawiać jest dostępny na GitHub-ie. 

### [github.com/mmotel/ng-beers-app](https://github.com/mmotel/ng-beers-app)

Aby rozpocząć pracę z aplikacją należy wykonać poniższe komendy.

```sh
git clone https://github.com/mmotel/ng-beers-app
cd ng-beers-app
npm install
git checkout v0
ng serve
```

Aplikacja jest podzielona na kroki oznaczone tagami. W trakcie tego szkolenia przyjrzymy się następującym tagom:

```
v11             LocalStorageService
v24             services providers in modules
v25             cache in service
v26             REST API Client
v27             custom pipe
v28             custom attribute directive
```

