# Data Fixtures ve Faker class kullanimi 

> Data Fixture en basitinden gelistirme ortaminda veritabanina sahte veri yukler ve biz de bu verileri kullanarak pagination, yerlestirme gorunum gibi islemleri yapariz. Son derece kullanislidir.

```bash
 $ composer require --dev doctrine/doctrine-fixtures-bundle
```

> /src altinda DataFixtures klasoru olusur

```php
// src/DataFixtures/AppFixtures.php
namespace App\DataFixtures;

use App\Entity\Product;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Persistence\ObjectManager;

class AppFixtures extends Fixture
{
    public function load(ObjectManager $manager)
    {
        // create 20 products! Bam!
        for ($i = 0; $i < 20; $i++) {
            $product = new Product();
            $product->setName('product '.$i);
            $product->setPrice(mt_rand(10, 100));
            $manager->persist($product);
        }

        $manager->flush();
    }
}
```
`Daha sonra $ php bin/console doctrine:fixtures:load komutu calistirilarak veriler database e yuklenir` once daha onceden bulunan veriler silinir. Sonra yenileri yuklenir.

`$ php bin/console doctrine:fixtures:load --append ` bu komut da databasede olan datalarin uzerinde yeni datalari ekler.

<br>

`Surekli ayni datalar olmasin derseniz PHP Faker componentini kullanabilirsiniz!`

```bash
    $ composer require fzaninotto/faker
```

<br>

> Faker icin isim ~ adres ~ numara gibi ozel verileri de kullanabilrsin. Check https://github.com/fzaninotto/Faker

```php
    // src/DataFixtures/AppFixtures.php
    namespace App\DataFixtures;

    use App\Entity\Product;
    use Doctrine\Bundle\FixturesBundle\Fixture;
    use Doctrine\Persistence\ObjectManager;
    use Faker\Factory;

    class AppFixtures extends Fixture
    {
        public function load(ObjectManager $manager)
        {
            $faker = Factory::create(); // faker objsi olusturuldu.

            // create 20 products! Bam!
            for ($i = 0; $i < 20; $i++) {
                $product = new Product();
                $product->setName($faker->text(20)); // 20 karakter uzunlugunda text rastgele 
                $product->setPrice(mt_rand(10, 100)); 
                $manager->persist($product);
            }

            $manager->flush();
        }
    }
```
