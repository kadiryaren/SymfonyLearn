# Many To Many iliskisi

Many to many en basitinden bir ogrencinin birden fazla derse kaydolabilmesi ile ayni iliskidir. Her ogrenci birden fazla derse kaydolabilir ve her derste de birden fazla ogrenci olabilir. 

`SF kodlamasi acisindan tek fark controller icerisinde birden fazla ogrenci objesi ve birden fazla sinif objesinin gerekli setter fonksiyonuna istenilen objenin verilmesinden ibarettir.`


```php
    
    /**
     * @Route("/ogrenci", name="ogrenci")
     */
    public function index(): Response
    {
       $ogrenci1 = new Ogrenci();
       $ogrenci1->setName('Ali');

       $ogrenci2 = new Ogrenci();
       $ogrenci2->setName('Mehmet');
       

       $ders1 = new Ders();
       $ders1->setName('Matematik');

       $ders2 = new Ders();
       $ders2->setName('Fizik');

       $ogrenci1->addDers($ders1);
       $ogrenci1->addDers($ders2);


       $ders1->addOgrenci($ogrenci1);
       $ders1->addOgrenci($ogrenci2);


        $ders2->addOgrenci($ogrenci1);
        $ders2->addOgrenci($ogrenci2);


        // relates this ogrenci to the sinif
        $ogrenci->setSinif($sinif1);

        $entityManager = $this->getDoctrine()->getManager();
        $entityManager->persist($ders1);
        $entityManager->persist($ders2);
        $entityManager->persist($ogrenci1);
        $entityManager->persist($ogrenci2);
        $entityManager->flush();

        return new Response('');
    }
```
