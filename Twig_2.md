# Twig part 2 (f i l t e r s)

##### ABS (mutlak deger) value degerini pozitif basar 
```twig
	{{ value|abs }}
```

##### Capitalize ⇒ Bas harfini buyuk yazar
```twig
	{{ value|capitalize }}
```

##### Date ==> php den Date objesi gonderilirse bu sekilde bastirilir.
```twig
	{{ value|date }} // default
	{{ value|date('M D Y') }} // costumize edilebilir. 
```


##### first ==> liste[0]   listenin ilk elemanini bastirir
```twig
	{{ liste|first }} 
```
##### last ⇒ liste[-1]   listenin son elemanini doner
```twig
	{{ liste|last }} 
```

##### join  ==>  string array icindeki elemanlari birlestirip string doner. parametre verilirse stringler arasina verilen parametreyi koyar.
```twig
	{{ liste|join }} //default
	{{ liste|join(',') }} 
```

##### keys ==> array degerlerinin key kisimlarini alir array doner. 
```twig
	{{ liste|keys }} 
```
```twig
	{{ liste|keys|join }} // ardisik islemler de yapilabilir. 
```

##### length  ⇒ arraydaki elemanlarin sayisini verir
```twig
	{{ liste|length }} 
```

##### lower  ⇒  stringi lowercase basar (hic buyuk harf yok )
```twig
	{{ string|lower }} 
```

##### merge ==> arrayi birlestirebilirsin 
```twig
	{{  liste|merge(["eleman"])|join(" ") }} // listenin sonuna eleman ekler ve basar  
```

#####  raw ==> twig normalde html scripti verirsen onu encode eder ve taglar dahil her seyi gosterir yani execute etmez o html kodunu 
##### ama raw sayesinde verilen html kodunu direk iceri sokup execute edebilirsiniz.
```twig
	{{  string|raw }} 
```

##### reverse  ⇒ listeyi tersine cevirir 
```twig
	{{  liste|reverse|join }} 
```

##### sort   ⇒ listeyi alfabetik siralar
```twig
	{{  liste|sort|join }} 
```

##### trim   ⇒ string degerin gereksiz bastan sondan bosluklarini siler.
```twig
	{{  string|trim|join }} 
```

#####  upper   ⇒ stringn butun karakterlerini buyuk harf yapar basar
```twig
	{{  string|upper }} 
```

#####  url_encode   ⇒ stringn url encode haline getirir
```twig
	{{  'https://github.com/?token=12345'|url_encode }} 
```


#####  json_encode   ⇒ stringn json encode haline getirir yani [array] halinden { json }  haline cevirir.
```twig
	{{  liste|json_encode }} 
```
