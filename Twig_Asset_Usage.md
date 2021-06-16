# Twig Asset Kullanimi/Yonetimi

> Temel olarak js css ve media dosyalari public/css - public/js veya public/images gibi public altindaki klasorlerde bulunurlar.


import ederken: 
```php

    <link href="{{ asset('css/main.css') }}" rel="stylesheet"> // seklinde cagrilabilir.
```

```php
    <script href="{{ asset('js/main.js') }}"></script> // seklinde cagrilabilir.
```
