# What is a route?
The specifier which describes a route for any given website, is based off of the path section of a URI address. The path parts as they are known in the 
URI standard comprise of three distinct forms. The constant, parameter and finally catch all.

1. Constant, example: ``/admin``
2. Parameter, example: ``/search/:keyword``
3. Catchall, example: ``/*``

Together when combined can produce the following routes:

* ``/products/:id``
* ``/products/:id/:action``
* ``/*`` where HTTP status code == 404 (page not found)
* ``/products/*`` where HTTP status code == 404
* ``/~NickH/pets/treats``
* ``/~NickH/pets/:name``

These specifications will be tested against URIs being sent from a client. These do not include the parameter specifier or have to respect the name in 
the specification. Instead these values get replaced with the parameter value. Constants are matches as is and finally a catch all will match against any 
path parts at and down the list. An example of this is ``/products/something/goes/here`` where the route specifier is ``/products/*``.

Route specifications may not always take this above form, but the purpose of the encoding will allow the above. Some specifications will support 
arbituary parameter validation at the router level. An example of parameter validation is regex based routers that allow for regex inputs without input 
validation (to remove anything other than constants).

The routes as described above does not include a pattern and can be quite arbituary. Many different pattern styles exist, ASP.net has two default 
router patterns. The first is ``{controller}/{action}/{id}`` an example of this is ``/Products/show/beverages``. The second is 
``{resource}.axd/{*pathInfo}`` which is an implementation specific pattern.
Not all web service frameworks define patterns as best practice (or supply it by default). Ruby on Rails is an example of a web service framework that 
primarily uses an arbituary route pattern.
