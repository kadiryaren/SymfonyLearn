# Twig Extension Olusturma 
> Istenilen fonksiyon twig extension sayesinde twige eklenebilir.

<br>

Oncelikle src/ altina Twig adinda bir directory olusturuyoruz. Sonra bunun icine `AppExtensions.php` dosyasini olusturuyoruz. 

```php
// src/Twig/AppExtension.php

<?php

namespace App\Twig;

use Twig\Extensions\AbstractExtension;
use Twig\TwigFilter;

class AppExtension extends AbstractExtension
{
    // getFilters() methodu ilk yazilmasi gereken method ve yazacagimiz fonksiyonlari bi nevi tanimladigimiz yer. 
    public function getFilters(){
        return TwigFilter('md5',[$this,'functionName']);  // md5 yazan string twig icindeki  filtrenin adi ~~ functionName yazan kisimdaki fonskiyon adi da simdi bu dosyanin icinde olusturacagimiz md5 islemini yapan fonksiyonun adi. 

    }

    public function md5Filter($string){    // md5 ==> functionName 
        return md5($string);
    }
}

```
