# Doctrine

> Entity classlarindaki setter fonksiyonlari her zaman return $this;  seklinde geri donus yapacak sekilde ayarlamak gerekli. 

<br>

Select iki sekilde yapilabilir: Ileride detaylarini gorecegiz :
```php
// basit yolu 
    /*
    * @Route('/urunler/{id}', name='urun_show')
    */

    public function show(Urun $urun){
        // Basit bir sekilde urlden gelen urun idsine ait urun objesini alir ve kullanima sunar
        return new Response(urun->getId());
    }
```

```php
// entity manager ile kullanimi 
    /*
    * @Route('/urunler/{id}', name='urun_show')
    */

    public function show($id){
        $urunRepository = $this->getDoctrine()->getRepository(Urun::class); 
        // once repository olusturulur. Daha sonra find ile IDye ait row obje olarak getirilir.
        $urun = $urunRepository->find($id);

        return new Response($urun->getId());
    }
```

<center><h1>Insert(ekleme)</h1></center>

<br>

```php
// src/Controller/ProductController.php
namespace App\Controller;

// ...
use App\Entity\Product;
use Doctrine\ORM\EntityManagerInterface;
use Symfony\Component\HttpFoundation\Response;

class ProductController extends AbstractController
{
    /**
     * @Route("/product", name="create_product")
     */
    public function createProduct(): Response
    {
        // you can fetch the EntityManager via $this->getDoctrine()
        // or you can add an argument to the action: createProduct(EntityManagerInterface $entityManager)
        $entityManager = $this->getDoctrine()->getManager();

        $product = new Product();
        $product->setName('Keyboard');
        $product->setPrice(1999);
        $product->setDescription('Ergonomic and stylish!');

        // tell Doctrine you want to (eventually) save the Product (no queries yet)
        $entityManager->persist($product);

        // actually executes the queries (i.e. the INSERT query)
        $entityManager->flush();

        return new Response('Saved new product with id '.$product->getId());
    }
}
```

<center><h1>Fetch (select)</h1></center>

```php
    /**
     * @Route("/product/{id}", name="product_show")
     */
    public function show(int $id): Response
    {
        $product = $this->getDoctrine()
            ->getRepository(Product::class)
            ->find($id);

        if (!$product) {
            throw $this->createNotFoundException(
                'No product found for id '.$id
            );
        }

        return new Response('Check out this great product: '.$product->getName());

        // or render a template
        // in the template, print things with {{ product.name }}
        // return $this->render('product/show.html.twig', ['product' => $product]);
    }

```

<br>

## Single object, Multiple object or All data 




```php
    $repository = $this->getDoctrine()->getRepository(Product::class);

    // look for a single Product by its primary key (usually "id")
    $product = $repository->find($id);

    // look for a single Product by name
    $product = $repository->findOneBy(['name' => 'Keyboard']);
    // or find by name and price
    $product = $repository->findOneBy([
        'name' => 'Keyboard',
        'price' => 1999,
    ]);

    // look for multiple Product objects matching the name, ordered by price
    $products = $repository->findBy(
        ['name' => 'Keyboard'],
        ['price' => 'ASC']
    );

    // look for *all* Product objects
    $products = $repository->findAll();

```

## ParamConverter Kullanarak path id girilene gore datayi almak 

```bash
    $ composer require sensio/framework-extra-bundle
```

```php
        /**
        * @Route("/product/{id}", name="product_show")
        */
        public function show(Product $product): Response
        {
            // Burada girilen id ile eslesen $product objesini kullanabilirsin.
            // ...
        }
```

> ParamConverter nasil degisik sekillerde kullanilabilir?

```php

    /**
    * @Route("/product/{id}", name="product_show")
    * @ParamConverter("product", options={"id" = "product_object"})
    * // artik Product $product degil de $produxt_object olarak da cagirabiliriz.
    */
    public function show(Product $product): Response
    {
        // Burada girilen id ile eslesen $product objesini kullanabilirsin.
        // ...
    }

```
<center><h1>Update</h1></center>

<br>

```php
    /**
     * @Route("/product/edit/{id}")
     */
    public function update(int $id): Response
    {
        $entityManager = $this->getDoctrine()->getManager();
        $product = $entityManager->getRepository(Product::class)->find($id);

        if (!$product) {
            throw $this->createNotFoundException(
                'No product found for id '.$id
            );
        }

        $product->setName('New product name!');
        $entityManager->flush();

        return $this->redirectToRoute('product_show', [
            'id' => $product->getId()
        ]);
    }
```

<center><h1>Delete</h1></center>

<br>

> Find and delete it.

```php
    $entityManager->remove($product);
    $entityManager->flush();
```
