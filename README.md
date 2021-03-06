# ionicng2-currency-mask

A very simple currency mask directive for Angular that allows using a number attribute with the ngModel. In other words, the model is a number, and not a string with a mask. It was tested in Angular version 4 and 5.

Note: This component is ready to AoC (Ahead-of-Time) compilation.

## Getting Started

### Installing and Importing

Install the package by command:

```sh
    npm install ionicng2-currency-mask --save
```

Import the module

```ts
import { CurrencyMaskModule } from "ionicng2-currency-mask";

@NgModule({
    imports: [
        ...
        CurrencyMaskModule
    ],
    declarations: [...],
    providers: [...]
})
export class AppModule {}
```

### Using 

```html
    <ion-input currencyMask [(ngModel)]="value" [(ngModelMoney)]="value2" />
```

 * `ngModel` An attribute of type number. If is displayed `'$ 25.63'`, the attribute will be `'25.63'`.

### Options 

You can set options as follows:

```html
    <!-- example for pt-BR money -->
    <ion-input currencyMask [(ngModel)]="value" [options]="{ prefix: 'R$ ', thousands: '.', decimal: ',' }"/>
```

Available options: 

 * `align` - Text alignment in input. (default: `right`)
 * `allowNegative` - If `true` can input negative values.  (default: `true`)
 * `decimal` -  Separator of decimals (default: `'.'`)
 * `precision` - Number of decimal places (default: `2`)
 * `prefix` - Money prefix (default: `'$ '`)
 * `suffix` - Money suffix (default: `''`)
 * `thousands` - Separator of thousands (default: `','`)

You can also set options globally...

```ts
import { CurrencyMaskModule } from "ng2-currency-mask";
import { CurrencyMaskConfig, CURRENCY_MASK_CONFIG } from "ng2-currency-mask/src/currency-mask.config";

export const CustomCurrencyMaskConfig: CurrencyMaskConfig = {
    align: "right",
    allowNegative: true,
    decimal: ",",
    precision: 2,
    prefix: "R$ ",
    suffix: "",
    thousands: "."
};

@NgModule({
    imports: [
        ...
        CurrencyMaskModule
    ],
    declarations: [...],
    providers: [
        { provide: CURRENCY_MASK_CONFIG, useValue: CustomCurrencyMaskConfig }
    ],
    bootstrap: [AppComponent]
})
export class AppModule {}
```

### Validation

This directive also provides built-in validation for minimum and maximum values. If the attributes 'min' and / or 'max' are setted, the Angular CSS class 'ng-invalid' will be added to the input to indicate an invalid value.

```html
    <ion-input currencyMask [(ngModel)]="value" min="-10.50" max="100.75" />
```

## Quick fixes

### Ionic 2-3

Input not working on mobile keyboard

```html
<!-- Change the type to 'tel' -->
    <ion-input currencyMask type="tel" [(ngModel)]="value" />
```

Input focus get hide by the mobile keyboard

on HTML
```html
<!-- Change the type to 'tel' -->
    <ion-input currencyMask type="tel" [(ngModel)]="value" [id]="'yourInputId' + index" (focus)="scrollTo(index)" />
```

on .ts
```ts
import { Content } from 'ionic-angular';

export class...

    @ViewChild(Content) content: Content;
  
    scrollTo(index) {
        let yOffset = document.getElementById('yourInputId' + index).offsetTop;
        this.content.scrollTo(0, yOffset + 20);
    }
```

## Based on the library by Cesarrew ng2-currency-mask
https://github.com/cesarrew/ng2-currency-mask

