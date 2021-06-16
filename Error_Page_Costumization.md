# Error Page Costumization

> Herhangi bir bundle icindeki twig sayfalarini ozellestirmek icin; O bundle icerisindeki view sayfasinin klasor yapisini aynen olusturmaliyiz(templates klasoru icinde). 


```
    templates + bundleName + (bundle altinda ki view klasorunun alt yapisi ile ayni olacak) + Exceptions + twigFile 

    templates/bundles/TwigBundle/Exceptions/error.html.twig  // veya error[statusCode].html.twig
    error502.html.twig
```

