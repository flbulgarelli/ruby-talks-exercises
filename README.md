# Ejercicios

## Introducción

Estos son algunos ejercicios de Ruby. Los temas que tratan son

 * Expresiones: evaluación de expresiones en general
 * File Path: String Interpolation y Env Variables
 * Arbol Binario: Modelado, Bloques, Mixin Enumerable, Enumerator, RSpec, Regexp
 * Select: Colecciones, bloques, RSpec
 * Suma de Mapas: OpenClasses, Alias
 * Numeros Romanos: Modelado
 * Variables, Variables, Variables: Que imprime esto?
 * Guía de teléfonos REST: Sinatra, DataMapper
 * DSL Equipos de Fútbol: Todo
 * OpenStruct: MethodMissing 
 * Distribuidores de Cerveza: MethodMissing, Send, Regexp
 * URLEncoded: OpenClasses
 * Basic Metapogramming: Misc


## Expresiones: Cual es valor de las siguientes expresiones?


```ruby
x = []
5 if x.empty?
```


```ruby
x = 6
def bar(x) 
  x = 7
  x
end
bar(6)
x
```

```ruby
def foo 
 [4, 5]
end
```


```ruby
puts  "hello"
```

```ruby
x = 50
[ (if x >  40; 'foo'; else 'bar'; end), ('foobar' unless x > 30) ]
```


```ruby
class Bar 
 4
end
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

```

## File Path

Definir una función que dado un nombre de archivo, y un directorio relativo al home dir del usuario, devuelva el path absoluto del archivo. No usar concatenación de Strings. 

## Select 

a. Implementar ```select```: es un mensaje que filtra una colección, devolviendo un ```Array``` con los elementos que cumplen una condición dada.

b. Especificar select mediante RSpec

  
## Arbol Binario

Se desea modelar un arbol binario, en el que tanto las hojas como nodos contienen un valor. 

a. Se desea poder imprimir cada uno de los elementos del arbol, usando recorrido primero en profundidad. 

```ruby
my_tree.to_s
```

y que esto devuelva el string,  ```"[5, 1, 200, 45]"```

b. Implementar un metodo para ejecutar un bloque por cada elemento del arbol. Refactorizar ```to_s``` para que lo use. 

c. Refactorizar el código para usarlo como una coleccion estandar de Ruby (ver Enumerable). Ejemplo:

```ruby
my_tree.select { |x| x > 5 }
```

d. Implementar ahora un método para recorrido primero en amplitud. Sin romper el código anterior, mostrar como se podría utilizar este método para a partir del mismo obtener obtener los métodos de Enumerable. (ver Enumerator)

e. Implementar lo necesario para que yo pueda hacer lo siguiente con los métodos de Enumerable (por ejemplo, select):

```ruby
my_tree dp_select { ..condicion... } #como ya lo habiamos hecho, select empleando deep first
my_tree select { ..condicion..  } #equivalente a dp_select
my_tree bf_select { ...condicion ... } #igual select, pero empleando breadth first
```

Tip: Aprovechar para probar regexps. 

f. Crear una especificacion con RSpec para el arbol. 

## Suma de Mapas

Escribir el código necesario para poder implementar las union de mapas mediante el mensaje +:

Ej:

```ruby
irb(main):023:0>  {:foo => 4} + {:bar => 6}
=> {:foo=>4, :bar=>6}
```
Tips: explorar la doc de Hash. Hay MUCHA alternativas. Investigar ```alias```.

## Numeros Romanos

Implementar un conversor de numeros arabigos a romanos. Debe funcional al menos hasta el 4999

## Variables, Variables, Variables: Que imprime esto?

```ruby
class A
 @@var = 1

 class << self
   attr_reader :var
 end
end
class B < A
@@var = 2

end
class C < A
@@var = 3

end

puts A.var
puts B.var
puts C.var
```


## Guía de teléfonos REST

Se desea implementar una guía de teléfonos, que me paremita saber las siguientes cosas:

 * dado un teléfono, a quien pertence (id, nombre, apellido), la empresa proveedora y su domicilio.
 * búsqueda reversa: dado un nombre y apellido, obtener el teléfono y la información anterior
 * saber la cantidad de abonados totales, y por empresa

a. Exponer estas funcionalidad via REST empleando Sinatra

b. Se desea autenticar el API de forma que solo los usuarios registrados puedan acceder a la misma. 
Agregar autenticacion HTTP básica, y exponer la funcionalidad necesaria para que el usuario pueda actualizar agregar teléfonos (propios) adicionales, y para que se puedan consultar dichos teléfonos para un usuario. 

d. Persistir el modelo en una base de datos relacional (ej: sqlite) con Data Mapper.


## DSL Equipos de Fútbol
Implementar un DSL para organizar partidos de futbol. El DSL debe contar con construcciones para:
 * definir los equipos y miembros de cada uno (cada miembro del equipo se identifica por un apodo)
 * definir los encuentros (cancha, día, hora, condcion climatica)
 * indicar los resultados de cada encuentro (como salio el partido, las condiciones climaticas, los hechos salientes)

Con estas definiciones cargadas, yo deberia poder interpretar mi lenguaje futbolistico y poder obtener estadísticas, sugerencias, etc (esto está uera del ejercicio, con plantear una estadística simple como porcentaje de partidos ganados por cada equipo alcanza)

Tip: usar la imaginación, el DSL resultante tiene que ser mas que una fluent api, explotar las características de metaprogramación. Es decir, el DSL no se debería ver como:

```ruby
def setup do
  equipo1 = Equipo.new
  equipo1.nombre = '...'
  equipo1.integrantes = [ 'tyny', 'cono', 'guido', ...]
end
```

sino mas bien y por dar un ejemplo:

```ruby
equipo 'equipo1' do
  integrantes :tyny, :cono, :guido 

end
```

## OpenStruct 

OpenStruct es una clase bastante útil para definir dtos, similar a un Hash, pero con la diferencia de que en lugar de acceder mediante el mensaje [] a los valores, lo hago empleando accessors normales. Ej:

```ruby
require 'ostruct'

hash = {:foo => 4, :bar => []}
ostruct = OpenStruct.new( :foo => 4, :bar => [] )

hash[:foo] vs ostruct.foo 
hash[:baz] = 4 vs ostruct.baz = 4
```

OpenStruct no soporta ningun otro compartimiento además de estos dos (ej, no entiende los metodos iteradores). 

a. Implementar ```OpenStruct```

b. Agregar la siguiente mejora de performance: cachear los métodos. 

 Tip: La primera vez que se evalua el method missing, agregar un método nuevo. Los envios subsiguientes de ese mensaje no daberían resultar en la evaluacion de method missing. 



## Validaciones

a. Implementar un mecanismo similar a ```attr_accessor```, llamado ```attr_check_not_null```, que genere los getters y setters, pero además, valide en el setter que el argumento es no nulo.

b. Generalizar la solucón a ```attr_check```, que tome otro argumento que sea la condición a validar en el setter

## Distribuidores de Cerveza

OpenBeer es un protocolo abierto y ficticio para la distribución de cerveza, implementado por varias conocidas cervezerías,  y también, por algunos cerveceros caseros. El protocolo define a una BeerDistributor como un objeto que entiende al menos un mensaje de la forma:

```ruby
submit_beer_request(beer_request, callback)
```

El beer request es un hash con la cantidad de botellas, la direccion, y otros detalles que no nos interesan por ahora.

Como los pedidos son asincronicos, el callback es un bloque que será evaluado cuando el cargamento esté listo para ser enviado, al cual se le pasarán un objeto que sabe cobrar y entiende mensaje de la siguiente forma:

```ruby
pay_for_beer(payment)
```

Si el pago no se efectua, por la cantidad correcta, la compra se cancela.

Se pide: 

a. implementar un comprador de cerveza compulsivo, que cada vez que cobra una cierta suma de dinero, compra cerveza hasta que se agoten sus ahorros.     

b. Implementar un test unitario. Mockear al BeerDistributor. 

c. Por una disposicion legal, todos los compradores de cerveza de ahora en más tienen que loguear el ```beer_request``` cada vez que hagan un ```submit_beer_request```. Resolverlo de forma transparente para los compradores (ej: no hay que modificar el codigo del comprador compulsivo)

d. OpenBeer 2.0 agrega soporte para la distribucion de cervezas de distintos tipos, picadas, pancitos y demases. Esta nueva version define 35 métodos nuevos, de la forma:

```ruby
submit_picada_request(picada_request, callback)
submit_bock_beer_request(bock_beer_request, callback)
```

etc...

Hacer los cambios necesarios para que todos estos requests sean logeados conforme a la reglamentación vigente. 

Tip: Usar regexps. 

## URLEncoded

Hacer lo necesario para que todos los objetos, incluso los ya provistos por Ruby u otras bibliotecas, entiendan el mensaje ```to_base64```, que debe devolver el mismo resultado que ```to_s```, pero encodeado en Base64

## Basic Metapogramming

 * [http://ruby-metaprogramming.rubylearning.com/html/Exercise_4.html] Nota: p es un comando de irb. Que hace?
 * [http://ruby-metaprogramming.rubylearning.com/html/Exercise_2.html]
 * [http://ruby-metaprogramming.rubylearning.com/html/Exercise_1.html](Desafío del café con leche)


## TODOs

 * eigent classes
 * clobs
 * http://www.rubyquiz.com/quiz32.html
 * http://www.rubyquiz.com/quiz8.html
 * http://www.rubyquiz.com/quiz7.html
 * http://www.rubyquiz.com/quiz155.html
 * http://www.rubyquiz.com/quiz9.html

 