
# Bir bundle in belirli bir parcasini yeniden yazmak @Override
`Burada sadece Template Override ve Controller Override Anlatilmistir. Diger Overridelar icin Google layin ;)`

<br>

Bir Bundle indirdiniz veya olusturdunuz kullaniyorsunuz fakat uzerinde degisiklik yapmak istiyorsunuz. Eger bu degisikligi direk (indirdi iseniz) vendor altinda yaparsaniz, guncellemelerden sonra yaptiginiz degisiklik kaybolur fakat kendi proje dizininizin altinda gerekli klasor yapilarini bundle klasor yapisi ile ayni olacak sekilde ayarlar isek SF bize uzerinde override yapma imkani taniyor. Ornek olarak template uzerinde bir degisiklik yapilacak olsun. 

<br>


> Default Bundle Template ==>  /vendor/symfony/bundle-name/Resources/views/index.html.twig olsun 

<br>

Bu durumda ana dizinimizdeki /templates klasorunun altina /bundles adinda folder olusturuyoruz. 
Daha sonra default dizindeki klasor yapisini birebir kopyaliyoruz(bundle ismi ile birlikte) .

<br>

> /templates/bundles/bundle-name/Resources/views/index.html.twig 

<br>

Artik Bu dosyanin icine ne yazarsak bu bizim icin gecerli olacaktir. `Controller icerisinde de degisiklik yapmaya gerek yok. $this->render(icerigi ayni kalacak) symfony template klasorunun icinde ayni klasor yapisi oldugundan bizim yazmis oldugumuzu alip kullanacak`.


<br>

> Eger Controller Override etmek istiyorsak da /config altinda anotations.yaml vardi hatirlarsaniz. Onun icerisine bizim Controller ust satirlarda kalacak sekilde gerekirse yer degisikligi yapilmalidir.

```php
// annotations.yaml 
// Bu sekilde bizim ana /src/Controller ayarimiz ustte olacak sekilde yazabiliriz.


controller:
    resource: ../../src/Controller;
    type: annotation

test-bundle-controller:
    resource: ../../src/Test/TestBundle/Controller;
    type: annotation    
```

<br>

> Diger kisimlardaki overridelar da gerekli dizin yapilari taklit edildikten sonra kullanilabilir.

