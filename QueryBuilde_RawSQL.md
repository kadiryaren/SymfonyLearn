# QueryBuilder ile query olusturmak 

Find, FindAll ve FindBy gibi cagrilar yetmedigi zaman Repository icerisine kendimiz fonksiyonlar yazabiliriz. 


```php
    // src/Repository/ProductRepository.php

    // ...
    class ProductRepository extends ServiceEntityRepository
    {
        public function findAllGreaterThanPrice(int $price): array
        {
            // automatically knows to select Products
            // the "p" is an alias you'll use in the rest of the query
            $qb = $this->createQueryBuilder('p')
                ->where('p.price > :price')
                ->setParameter('price', $price)
                ->orderBy('p.price', 'ASC')
                ->getQuery();

            return $qb->execute(); 
            // return $qb->execute();  bu ifade aslinda geri donen select isleminin datalari ve array halinde doner.

            // to get just one result:
            // $product = $query->setMaxResults(1)->getOneOrNullResult();
        }
    }
```


<br>

# Saf SQL calistirmak

`herhangi bir parametre verilmeksizin sql calistirmak:`

```php
// src/Repository/ProductRepository.php

// ...
class ProductRepository extends ServiceEntityRepository
{
    public function findAllGreaterThanPrice(int $price): array
    {
        $conn = $this->getEntityManager()->getConnection();

        $sql = '
            SELECT * FROM product p
            WHERE p.price > 50
            ORDER BY p.price ASC
            ';
        $stmt = $conn->prepare($sql);
        $stmt->execute();

        // returns an array of arrays (i.e. a raw data set)
        return $stmt->fetchAllAssociative();
    }
}

```

<br>

` parametre ile sql calistirmak:`

```php
// src/Repository/ProductRepository.php

// ...
class ProductRepository extends ServiceEntityRepository
{
    public function findAllGreaterThanPrice(int $parameter): array
    {
        $conn = $this->getEntityManager()->getConnection();

        $sql = '
            SELECT * FROM product p
            WHERE p.price > :parameter
            ORDER BY p.price ASC
            ';
        $stmt = $conn->prepare($sql);
        $stmt->execute(['parameter' => $paramter]);

        // returns an array of arrays (i.e. a raw data set)
        return $stmt->fetchAllAssociative();
    }
}

```
