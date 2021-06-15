# Twig part 1
```twig
  {% var|e %} // enable escape character 
```

### Yaptiginiz twig degisiklikleri calismiyorsa => 
```bash
  $ php bin/console cache:clear 
```
Ya da Linux icin:

```bash
  $ rm -rf var/cache/dev/*
```


### ?? Bundle icerisindeki twig dosyalarina erismek icin : 
```php
	return $this->render("@Security/Collector/security.html.twig"); 
	// yani dosya pathinin onune @ koyarak ulasiriz 
```

### ?? {% extends 'base.html.twig' %}  => "base html" i extend ederken kullaniriz.
### ?? {% include 'filename' %} ==> istenilen her twig file i bu sayede istenilen dosyanin icine gomulebilir.
==> Her yerde kullanilan bir buton vardir. Bu buton farkli bir twig file olarak olusturulur ve gerekli yerlerde include edilerek kullanilabilir. gibi gibi .

##### Block olusturma
```twig
	{% block blockAdi %}
	{% endblock %}
```
##### if blogu olusturma
```twig
	{% if  boolean %}
	// if boolean is defined(ozel key) // boolean degiskeninin controllerdan gonderilip gnderilmdigi check
	{% else %}
		// write something..
	{% endif %}
```


##### For blogu olusturma
```twig
	{% for  item in items %}
		<h1>{{ item }}</h1>     	// klasik pseudo for 
	{% endfor %}
```

##### php empty function 
```twig
	{% if variable is empty %}
		variable is empty
	{% else %}
		variable is not empty
	{% endif %}
```

##### null check function 
```twig
	{% if variable is null %}
		variable is null
	{% else %}
		variable is not null
	{% endif %}
```

##### tek cift check function 
```twig
	{% if 10 is even %}
		10 is even
	{% else %}
		10 is odd
	{% endif %}
```


##### array mi degil mi check 
```twig
	{% if variable  is iterable %}
		variable is iterable (yani array)	
	{% else %}
		variable is not iterable (yani array degil )	
	{% endif %}
```

##### array mi degil mi check 
```twig
	{% block set_test %}
		{% set variable = "text" %}
		{{ variable }}   // degiskeni twig icinde bu sekilde tanimlayabiliriz.
	{% endblock %}
```


##### Bosluklari silme Spaceless
```twig
	{% spaceless %}
		<div>
			<h1> deneme </h1>
		</div>
	{% endspaceless%}
	
	source code:
	<div><h1>deneme</h1></div>
```



