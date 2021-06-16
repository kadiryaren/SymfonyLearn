# Kendi Konsol Komutumuzu Yazalim `php bin/console`

Basit bir sekilde ekrana bizim belirledigimiz komut yazildiginda hello world yazan bir komut tasarlayalim!
Oncelikle /src altina Command adinda bir folder olustururuz.
Daha sonra dosyamizi olustururuz.

```php
    // src/Command/HelloCommand.php
    <?php

    namespace App\Command;

    use Symfony\Component\Console\Command\Command;
    use Symfony\Component\Console\Input\InputInterface;
    use Symfony\Component\Console\Output\OutputInterface;

    class HelloCommand extends Command{   
    // command olusturmak icin Command sinifini extend etmemiz lazim
    // iki adet default fonksiyon hazirlamamiz lazim

    protected function configure(){
        $this
            ->setName('app:hello')
            ->setDescription('Ekrana Hello World Bastirir')
            ->setHelp('php bin/console app:hello yazarsaniz ekrana hello world basar');

    }

    protected function execute(InputInterface $input, OutputInterface $output){
        $output->writeln('Hello World');

    }


    }

```
