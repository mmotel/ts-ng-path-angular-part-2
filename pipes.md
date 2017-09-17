# Potoki

![](/assets/pipe.png)

## wbudowane potoki

* [`DatePipe`](https://angular.io/api/common/DatePipe),
* [`JsonPipe`](https://angular.io/api/common/JsonPipe),
* [`CurrencyPipe`](https://angular.io/api/common/CurrencyPipe),
* [`DecimalPipe`](https://angular.io/api/common/DecimalPipe),
* [`PercentPipe`](https://angular.io/api/common/PercentPipe),
* [`SlicePipe`](https://angular.io/api/common/SlicePipe),
* [`LowerCasePipe`](https://angular.io/api/common/LowerCasePipe),
* [`UpperCasePipe`](https://angular.io/api/common/UpperCasePipe),
* [`TitleCasePipe`](https://angular.io/api/common/TitleCasePipe).

## customowe potoki

```js
@Pipe({name: 'exponentialStrength'})
export class ExponentialStrengthPipe implements PipeTransform {
  transform(value: number, exponent: string): number {
    let exp = parseFloat(exponent);
    return Math.pow(value, isNaN(exp) ? 1 : exp);
  }
}
```


---

###### Źródła

* https://angular.io/guide/pipes