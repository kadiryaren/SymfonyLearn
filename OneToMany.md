# OneToMany ~ ManyToOne Topic

`One To Many  <>  Many to One iliskisinin ters hali oldugu icin onu aciklamayacagim`

![One To Many](https://www.teach-ict.com/as_a2_ict_new/ocr/AS_G061/315_database_concepts/attributes_entities/miniweb/images/one2many.jpg)

<br>

`OneToMany`  bu iliski tipi anne cocuk iliskisine benzer. Bir annenin birden fazla cocugu olabilir ama bir cocugun tek annesi vardir. Veya guncel olarak her kullanicinin birden fazla gruba dahil olabildigi sistemleri dusunursek `One To Many` iliski tipini kullanabiliriz.

Farzedelim ki kategori ve urun iliskisi kurmaya calisiyoruz. Ve her bir urunun sadece bir kategorisi olabilir. Fakat her kategoride birden fazla urun olabilir. Bu durumda su sekilde bir yapi olusturulabilir: 


`many product to one category `


```php
    $ php bin/console make:entity Category

    New property name (press <return> to stop adding fields):
    > name

    Field type (enter ? to see all types) [string]:
    > string

    Field length [255]:
    > 255

    Can this field be null in the database (nullable) (yes/no) [no]:
    > no

    New property name (press <return> to stop adding fields):
    >
    (press enter again to finish)

```

```php
    // src/Entity/Category.php
    namespace App\Entity;

    // ...

    class Category
    {
        /**
        * @ORM\Id
        * @ORM\GeneratedValue
        * @ORM\Column(type="integer")
        */
        private $id;

        /**
        * @ORM\Column(type="string")
        */
        private $name;

        // ... getters and setters
}
```

```php
    $ php bin/console make:entity

    Class name of the entity to create or update (e.g. BraveChef):
    > Product

    New property name (press <return> to stop adding fields):
    > category

    Field type (enter ? to see all types) [string]:
    > relation

    What class should this entity be related to?:
    > Category

    Relation type? [ManyToOne, OneToMany, ManyToMany, OneToOne]:
    > ManyToOne

    Is the Product.category property allowed to be null (nullable)? (yes/no) [yes]:
    > no

    Do you want to add a new property to Category so that you can access/update
    Product objects from it - e.g. $category->getProducts()? (yes/no) [yes]:
    > yes

    New field name inside Category [products]:
    > products

    Do you want to automatically delete orphaned App\Entity\Product objects
    (orphanRemoval)? (yes/no) [no]:
    > no

    New property name (press <return> to stop adding fields):
    >
    (press enter again to finish)

```

```php
    // src/Entity/Product.php
    namespace App\Entity;

    // ...
    class Product
    {
        // ...

        /**
        * @ORM\ManyToOne(targetEntity="App\Entity\Category", inversedBy="products")
        */
        private $category;

        public function getCategory(): ?Category
        {
            return $this->category;
        }

        public function setCategory(?Category $category): self
        {
            $this->category = $category;

            return $this;
        }
    }
```

```php
    // src/Entity/Category.php
    namespace App\Entity;

    // ...
    use Doctrine\Common\Collections\ArrayCollection;
    use Doctrine\Common\Collections\Collection;

    class Category
    {
        // ...

        /**
        * @ORM\OneToMany(targetEntity="App\Entity\Product", mappedBy="category")
        */
        private $products;

        public function __construct()
        {
            $this->products = new ArrayCollection();
        }

        /**
        * @return Collection|Product[]
        */
        public function getProducts(): Collection
        {
            return $this->products;
        }

        // addProduct() and removeProduct() were also added
    }
```

## Kayit alma 

```php
    // src/Controller/ProductController.php
    namespace App\Controller;

    // ...
    use App\Entity\Category;
    use App\Entity\Product;
    use Symfony\Component\HttpFoundation\Response;

    class ProductController extends AbstractController
    {
        /**
        * @Route("/product", name="product")
        */
        public function index(): Response
        {
            $category = new Category();
            $category->setName('Computer Peripherals');

            $product = new Product();
            $product->setName('Keyboard');
            $product->setPrice(19.99);
            $product->setDescription('Ergonomic and stylish!');

            // relates this product to the category
            $product->setCategory($category);

            $entityManager = $this->getDoctrine()->getManager();
            $entityManager->persist($category);
            $entityManager->persist($product);
            $entityManager->flush();

            return new Response(
                'Saved new product with id: '.$product->getId()
                .' and new category with id: '.$category->getId()
            );
        }
    }
```

## Kayitlari cekme 

```php
    // src/Controller/ProductController.php
    namespace App\Controller;

    use App\Entity\Product;
    // ...

    class ProductController extends AbstractController
    {
        public function show(int $id): Response
        {
            $product = $this->getDoctrine()
                ->getRepository(Product::class)
                ->find($id);

            // ...

            $categoryName = $product->getCategory()->getName();

            // ...
        }
    }
```

