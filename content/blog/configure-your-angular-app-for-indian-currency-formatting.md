---
title: "Configure Your Angular App for Indian Currency Formatting"
date: 2019-10-09T08:57:22+05:30
Description: "A quick post on how to configure an Angular App that displays currencies formatted in Indian locale with symbol"
Tags: [angular, javascript, typescript]
Categories: []

---
# 

You can configure the Indian locale application wide by registering the **en-IN** locale using **registerLocaleData()** in the `app.module.ts`. You can also enable this only for a particular module by registering the locale in the specific module file. 

**`In app.module.ts:`**
<div class="code">
{{< highlight typescript >}}
import { registerLocaleData } from '@angular/common';
import localeIn from '@angular/common/locales/en-IN';
registerLocaleData(localeIn);
{{< / highlight >}} 
</div>

And in your template (html) file, apply the currency pipe with following arguments:

**`In home.component.html:`**
<div class="code">
{{< highlight javascript >}}
{{ amount | currency :'INR' : 'symbol' : '1.2-2' : 'en-IN' }}
{{< / highlight >}} 
</div>

**Hint**: the Currency pipe syntax used here is:
<div class="code">
{{< highlight javascript >}}
{{ value | currency : currencyCode : symbol : {minIntegerDigits}.{minFractionDigits}-{maxFractionDigits} : locale }}
{{< / highlight >}} 
</div>


This is how the formatted currency fields look like:

<img src="/images/angular-inr-currency-formatting.JPG" alt="Angular Currency Formatting In INR" class="responsive-post-image" style="border:1px solid #cdcdcd;"/>

You can find more details on the CurrencyPipe in the official <a href="https://angular.io/api/common/CurrencyPipe" target="_blank">Angular</a> docs.

