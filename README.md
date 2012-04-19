# Ejercicios


## Expresiones: Cual es valor de las siguientes expresiones?

```ruby
def foo 
 [4, 5]
end
```

```ruby
def bar(x) 
  x = 7
  x
end
```

```ruby
class Bar 
 4
end
```

```ruby
puts  "hello"
```

```ruby
x = []
5 if x.empty?
```

```ruby
x = 50
[ (if x >  40; 'foo'; else 'bar'; end), ('foobar' unless x > 30) ]
```

```ruby
x = 'foo'
x = x.reverse
x
```

```ruby
x = 'foo'
x.reverse!
x
```

```ruby 
'foo'.replace('bar') #que conclusion pueden sacar respecto a !?
```

```ruby
:foo == 'foo'
```

```ruby
:foo == :foo
```

```ruby
:foo.equal? :foo
```

```ruby
'hello'.equal? 'hello'
```

```ruby
'hello'.equal? 'hello'
```

```ruby
{:foo => 4}[:foo]
```

```ruby
{:foo => 4}['foo']
```
  
# Arbol Binario

Se desea modelar un arbol binario, en el que tanto las hojas como nodos contienen un valor. 

a. Se desea poder imprimir cada uno de los elementos del arbol, usando recorrido primero en profundidad. 

```ruby
my_tree.to_s
```

y que esto devuelva el string,  ```"[5, 1, 200, 45]"```

b. Implementar un metodo para ejecutar un bloque por cada elemento del arbol. Refactorizar ```to_s``` para que lo use. 

c. Refactorizar el código para usarlo como una coleccion estandar de Ruby. Ejemplo:

```ruby
my_tree.select { |x| x > 5 }
```

d. Crear una especificacion con RSpec para el arbol. 

## Numeros Romanos

Implementar un conversor de numeros arabigos a romanos. Debe funcional al menos hasta el 


Se desea implementar una guía de teléfonos, que me paremita saber las siguientes cosas:
  * dado un teléfono, a quien pertence (id, nombre, apellido), la empresa proveedora y su domicilio.
  * búsqueda reversa: dado un nombre y apellido, obtener el teléfono y la información anterior
  * saber la cantidad de abonados totales, y por empresa

a. Exponer estas funcionalidad via REST empleando Sinatra

b. Se desea autenticar el API de forma que solo los usuarios registrados puedan acceder a la misma. 
Agregar autenticacion HTTP básica, y exponer la funcionalidad necesaria para que el usuario pueda actualizar agregar teléfonos (propios) adicionales, y para que se puedan consultar dichos teléfonos para un usuario. 

d. persistir el modelo en una base de datos relacional con data mapper.


----------------
Implementar un DSL para organizar partidos de futbol. El DSL debe contar con construcciones para:
* definir los equipos y miembros de cada uno (cada miembro del equipo se identifica por un apodo)
* definir los encuentros (cancha, día, hora, condcion climatica)
* indicar los resultados de cada encuentro (como salio el partido, las condiciones climaticas, los hechos salientes)

Con estas definiciones cargadas, yo deberia poder interpretar mi lenguaje futbolistico y poder obtener estadísticas, sugerencias, etc (esto está uera del ejercicio, con plantear una estadística simple como porcentaje de partidos ganados por cada equipo alcanza)

Tip: usar la imaginación, el DSL resultante tiene que ser mas que una fluent api, explotar las características de metaprogramación. Es decir, el DSL no se debería ver como:


def setup do
  equipo1 = Equipo.new
  equipo1.nombre = '...'
  equipo1.integrantes = [ 'tyny', 'cono', 'guido', ...]
end

sino mas bien y por dar un ejemplo:

equipo 'equipo1' do
  integrantes :tyny, :cono, :guido 

end


---
string interpolation
-------------------
(OVERRIDE send)
Por convencion, ...


---
a. Implementar un mecanismo similar a attr_accessor, llamado attr_check_not_null, que genere los getters y setters, pero además, valide en el setter que el argumento es no nulo.
b. Generalizar la solucón a attr_check, que tome otro argumento que sea la condición a validar en el setter


-----
( send + method missing)
OpenBeer es un protocolo abierto (y ficticio :P) para la distribución de cerveza, implementado por varias conocidas cervezerías,  y también, por algunos cerveceros caseros. El protocolo define a una BeerDistributor como un objeto que entiende al menos un mensaje de la forma:

submit_beer_request(beer_request, callback)

El beer request es un hash con la cantidad de botellas, la direccion, y otros detalles que no nos interesan por ahora.

Como los pedidos son asincronicos, el callback es un bloque que será evaluado cuando el cargamento esté listo para ser enviado, al cual se le pasarán un objeto que sabe cobrar y entiende mensaje de la siguiente forma:

pay_for_beer(payment)

Si el pago no se efectua, por la cantidad correcta, la compra se cancela.

Se pide: 
a. implementar un comprador de cerveza compulsivo, que cada vez que cobra una cierta suma de dinero, compra cerveza hasta que se agoten sus ahorros.     
b. Implementar un test unitario. Mockear al BeerDistributor. 
c. Por una disposicion legal, todos los compradores de cerveza de ahora en más tienen que loguear el beer_request cada vez que hagan un submit_beer_request. Resolverlo de forma transparente para los compradores (ej: no hay que modificar el codigo del comprador compulsivo)
d. OpenBeer 2.0 agrega soporte para la distribucion de cervezas de distintos tipos, picadas, pancitos y demases. Esta nueva version define 35 métodos nuevos, de la forma:

submit_picada_request(picada_request, callback)
submit_bock_beer_request(bock_beer_request, callback)

etc...

Hacer los cambios necesarios para que todos estos requests sean logeados conforme a la reglamentación vigente. 

------------------
open classes + map


---
OpenStruct es una clase bastante útil para definir dtos, similar a un Hash, pero con la diferencia de que en lugar de acceder mediante el mensaje [] a los valores, lo hago empleando accessors normales. Ej:

require 'ostruct'


hash = {:foo => 4, :bar => []}
ostruct = OpenStruct.new( :foo => 4, :bar => [] )

hash[:foo] vs ostruct.foo 
hash[:baz] = 4 vs ostruct.baz = 4


OpenStruct no soporta ningun otro compartimiento además de estos dos (ej, no entiende los metodos iteradores). Implementar OpenStruct


----------
(Implementar mixin + redefinir send)

Desarrollar un Mixin Base64, tal que siempre que 

--> cosas con excepciones

--> cosas con strings 
    --> interpolacion
   --> strings "grandes"


Lesson 3: Collections & Bloques
 - bloques ({} y do .. end)
 - Que es un bloque?
   - llamar con bloque  
   - recibir un bloque
 - proc y lambda
 - Literales de lista y mapa
 - Iteratores de lista y mapa
  
Lesson 4: Modules

 - Definir un modulo
 - Modulo como namespace
 - Modulo como mixin
 - Mixins típicos de ruby

Lesson 5: Sum Up Example
 - Crear Ejemplo
 - Mostrar RSpec

Lesson 6: A Disgression on Dynamic Typing  ?

Parte 2:


4.send :+, 1

Lesson 7: Everything is an object
 - todo es un objeto
 - las clases son objetos
   - class instance variables
 - new no es una keyword reservada (instant factories)
 - siempre hay un self
 - scope gates

Lesson 8: Objects are about messaging
 - metodo send
 - method_missing
 - override responds_to

Lesson 9: Classes are Open!
 - Open Clases

Lesson 10: Eigenclasses is only a fancy name

Lesson 10: Metaprograming is just programming
 - define_method
 - instance_eval, class_eval
 - method hooks

