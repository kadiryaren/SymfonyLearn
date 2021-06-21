# Lets create own bundle!

> /src altina istedigimiz isimde bir directory olusturuyoruz. <br>
> /src/Test 

> Daha sonra Bundle ismimizle ayni isme sahip olan bir directory daha aciyoruz. /Test altina.<br>
> /src/Test/TestBundle


> Kendi bundle imizi symfony`nin tanimasi icin /TestBundle altinda bir php dosyasi olusturup gerekli tanimlamalari yapiyoruz. 


```php
<?php

namespace App\Test\TestBundle;

use Symfony\Component\HttpKarnel\Bundle\Bundle;

class TestBundle extends Bundle {

}

```

> Daha sonra bu bundle imizi bundle imizi /config/routes altindaki bundles.php dosyasina ekliyoruz. 

```php
// /config/routes/bundles.php
<?php

return[

    xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx,
    xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx,
    xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx,

    // Bizim bundle 
    // all, prod veya dev; bundle in hangi environmentlarda calisacagini soyler.
    // Mesela WebProfilerBundle prod ortaminda calismaz genellikle cunku gerek yok. 
    App\Test\TestBundle\TestBundle::class => ["all | prod | dev" => true]

];

```

### Peki bundle in klasor yapisi nasil olacak?

```
[+] src
    [+] Test
        [+] TestBundle
            [+] Controller
                [+] BundleTestController.php
            
            [+] Resources
                [+] config
                [+] public
                [+] views

            [+]Tests                
```

```php
// /BundleTestController.php

<?php 

namespace App\Test\TestBundle\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotations\Route;

class BundleTestController extends Controller{

    /*
    *   @Route('/test', name:'test')
    *   @return Response
    */

    public function Hello(){
        return new Response('hello bundle');
    }
}

```

> !!  BUNDLE ROUTING LERINI ENABLE ETMEK ICIN KENDI PROJEMIZE BIR KOD EKLEMEMIZ GEREKIR.

```php

// /config/routes/annotations.yaml

// dosya icindekilere ek olarak 

test-bundle-controller:
    resource: ../../src/Test/TestBundle/Controller;
    type: annotation
```
