# Kendi Konsol Komutumuza Option ve Arguman vermek

> Argumanlar sirali bir sekilde verilmelidir. Sira onemlidir. 

```bash
$ php bin/console app:hello first second third
```
<br>

> Options icin bu gecerli degildir. Zaten verilen degerin karsiligini veriririz.

```bash
$ php bin/console app:hello --option1="value1" --option3="value3"  --option2="value2"  
```

#### Arguman almak icin: 
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
                ->setHelp('php bin/console app:hello yazarsaniz ekrana hello world basar')
                ->addArgument($name, $mode, $description, $default); //  <<<<<-------
                // $name : Argumanin adi 
                // $mode : arguman required mi olacak yoksa optional mi olacak. 
                // $mode => InputArgument::OPTIONAL   or  InputArgument::REQUIRED   or 
                // $mode => InputArgument::IS_ARRAY 
                // $description : argumanin aciklamasi 
                // $default : arguman icin default value verilebilir. 

        }

        protected function execute(InputInterface $input, OutputInterface $output){
            $name = $this->getArgument('arguman adi'); // burada arguman degeri alinir.
            $output->writeln('Hello '.$name);

        }


    }

```

> -> $php bin/console app:hello --help  <- komutunu kullanarak argumanlariniza veya optionlariniza bakabilirsiniz.

> Optional olarak belirlenirse arguman default kismi verilebilir.

> IS_ARRAY seklinde verilirse degerlerin arasina bosluk konmasi yeterlidir. Geri donus degeri array olur.




<br><br>
### Option alma 

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
                ->setHelp('php bin/console app:hello yazarsaniz ekrana hello world basar')
                ->addOption('name','shortcut', mode, description, defaultValue);
                // shortcut "-y" seklinde verilmez direk "y" yazarsin terminalde -y olarak yazarsin. 
                // mode : InputOption::OPTIONAL  or  InputOption::REQUIRED  or InputOption::IS_ARRAY
                // desc: aciklama
                // defaultValue : default value
                

        }

        protected function execute(InputInterface $input, OutputInterface $output){
            $name = $this->getOption('option adi'); // burada option  degeri alinir.
            $output->writeln('Hello '.$name);

        }


    }
```
