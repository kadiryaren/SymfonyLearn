# Symfony RequestStack 
> Symfonyde gelen requestler RequestStack adinda bir obje tarafindan handle edilir. 
```php
	public function requestTest(RequestStack $requestStack){
		$request = $requestStack->request->getCurrentRequest();
		
		// $_POST islemleri icin
		$getPost = $request->request->get("nameOfParameter");
		
		// $_GET islemleri icin
		$getPost = $request->query->get("nameOfParameter");
		
		// $_COOKIE islemleri icin
		$getPost = $request->cookies->get("nameOfParameter");
		
		// attribute alma islemleri
		$getPost = $request->attributes->get("nameOfParameter");
		
		// $_FILES islemleri icin
		$getPost = $request->files->get("nameOfParameter");

		// $_SERVER islemleri icin
		$getPost = $request->server->get("nameOfParameter");

		// Header alma islemleri icin
		$getPost = $request->headers->all();
	
	}
```

### Farkli Tiplerde Response Donusleri 

```php
	return new Response("string");
	// OR 
	return new JsonResponse(["key" => "value"]);
	// OR 
	return $this->render("twigfile name");
	// OR
	return $this->redirectToRoute("name of controller route");
```



###  Servislere Controllerdan erismek 
* Direk Containera erisip ordan cekmek  ( Onerilmez! )
* veya Teker teker `use` kullanarak servisin yerini kullanip alabiliriz.

```php
public function service(SessionInterface $session){
	return new Response($session->getName());
}
```
