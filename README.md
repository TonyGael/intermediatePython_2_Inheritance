# Intermediate Python #2: Inheritance

La herencia es un concepto clave en la programación orientada a objetos (OOP) que permite a una clase heredar atributos y métodos de otra clase. En Python, la herencia se implementa de la siguiente manera:

1. **Clase Padre o Superclase:**
   - La clase que es heredada se conoce como la clase padre o superclase.
   - Contiene atributos y métodos que son compartidos por una o más clases derivadas.

2. **Clase Derivada o Subclase:**
   - La clase que hereda de otra clase se llama clase derivada o subclase.
   - Puede tener sus propios atributos y métodos adicionales, además de heredar los de la clase padre.

3. **Sintaxis de Herencia en Python:**
   - Para heredar de una clase, se especifica la clase padre entre paréntesis después del nombre de la clase derivada.

   ```python
   class ClasePadre:
       # Atributos y métodos de la clase padre

   class ClaseDerivada(ClasePadre):
       # Atributos y métodos adicionales de la clase derivada
   ```

   - La clase derivada puede acceder a los atributos y métodos de la clase padre y también puede agregar, modificar o anular (sobrescribir) sus propios atributos y métodos.

Ejemplo de herencia en Python:

```python
class Animal:
    def __init__(self, nombre):
        self.nombre = nombre

    def hacer_sonido(self):
        pass

class Perro(Animal):
    def hacer_sonido(self):
        return "¡Guau!"

class Gato(Animal):
    def hacer_sonido(self):
        return "¡Miau!"

# Crear objetos de las clases derivadas
mi_perro = Perro(nombre="Buddy")
mi_gato = Gato(nombre="Whiskers")

# Acceder a los atributos y métodos de la clase padre
print(f"{mi_perro.nombre} dice: {mi_perro.hacer_sonido()}")
print(f"{mi_gato.nombre} dice: {mi_gato.hacer_sonido()}")
```

En este ejemplo, `Animal` es la clase padre que tiene un método `hacer_sonido()`. Las clases `Perro` y `Gato` son clases derivadas que heredan de la clase `Animal`. Cada clase derivada implementa su propia versión del método `hacer_sonido()`.

La herencia permite la reutilización de código y facilita la organización y la estructura del código en proyectos más grandes. Además, promueve la coherencia y la consistencia al compartir funcionalidades comunes entre clases relacionadas.

# Intermediate Python #2: Operator Overloading

El "operator overloading" (sobrecarga de operadores) en Python se refiere a la capacidad de una clase para cambiar el comportamiento de los operadores incorporados, como la suma (+), la resta (-), la multiplicación (*), etc. Esto significa que puedes definir el comportamiento de estos operadores para objetos de tu propia clase. Es una característica de la programación orientada a objetos que proporciona una forma intuitiva de trabajar con tipos de datos personalizados.

Para implementar la sobrecarga de operadores en Python, puedes utilizar métodos especiales llamados métodos de operador o métodos mágicos. Estos métodos tienen nombres que comienzan y terminan con doble guion bajo (`__`). Algunos de los métodos de operador comunes son:

- `__add__`: Sobrecarga del operador de suma (`+`).
- `__sub__`: Sobrecarga del operador de resta (`-`).
- `__mul__`: Sobrecarga del operador de multiplicación (`*`).
- `__truediv__`: Sobrecarga del operador de división (`/`).
- `__eq__`: Sobrecarga del operador de igualdad (`==`).

Aquí hay un ejemplo simple que muestra cómo implementar la sobrecarga de operadores en una clase:

```python
class Punto:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, otro_punto):
        nuevo_x = self.x + otro_punto.x
        nuevo_y = self.y + otro_punto.y
        return Punto(nuevo_x, nuevo_y)

    def __eq__(self, otro_punto):
        return self.x == otro_punto.x and self.y == otro_punto.y

# Crear dos objetos de la clase Punto
punto1 = Punto(1, 2)
punto2 = Punto(3, 4)

# Sobrecarga del operador de suma
punto3 = punto1 + punto2
print(f"Suma de los puntos: ({punto3.x}, {punto3.y})")

# Sobrecarga del operador de igualdad
print(f"Los puntos son iguales: {punto1 == punto2}")
```

En este ejemplo, la clase `Punto` sobrecarga el operador de suma (`__add__`) para permitir la adición de dos objetos de tipo `Punto`. Además, sobrecarga el operador de igualdad (`__eq__`) para comparar la igualdad de dos puntos.

Es importante mencionar que la sobrecarga de operadores debe utilizarse con moderación y de manera intuitiva para evitar confusiones en el código. En general, se recomienda aplicarla solo cuando tenga sentido semántico para los objetos de la clase en cuestión.

# Script inheritance.py explicado:

Tu código define dos clases en Python, `Person` y `Worker`, que demuestran el concepto de herencia y la sobrecarga de métodos. Aquí hay una explicación paso a paso:

1. **Clase Person:**
   - La clase `Person` tiene un constructor (`__init__`) que inicializa los atributos `name`, `age` y `height`.
   - También define un método especial `__str__` para proporcionar una representación en cadena de la instancia de la clase.

2. **Clase Worker (que hereda de Person):**
   - La clase `Worker` hereda de la clase `Person`.
   - Tiene un constructor (`__init__`) que utiliza `super()` para llamar al constructor de la clase base (`Person`) y también inicializa el atributo adicional `salary`.
   - Sobrescribe el método `__str__` de la clase base (`Person`) para agregar información sobre el salario.
   - Introduce un nuevo método llamado `calc_yearly_salary` que calcula y devuelve el salario anual.

3. **Instancia de Worker:**
   - Se crea una instancia de la clase `Worker` llamada `worker_1` con valores específicos para `name`, `age`, `height` y `salary`.
   - Se imprime la representación en cadena de la instancia (`print(worker_1)`), que utiliza el método `__str__` sobrescrito para incluir información sobre el salario.
   - Se llama al método `calc_yearly_salary` y se imprime el resultado.

Aquí está el código con comentarios adicionales:

```python
class Person:
    def __init__(self, name, age, height):
        self.name = name
        self.age = age
        self.height = height

    def __str__(self):
        return "Name: {}, Age: {}, Height: {}".format(self.name, self.age, self.height)


class Worker(Person):
    def __init__(self, name, age, height, salary):
        super(Worker, self).__init__(name, age, height)
        self.salary = salary

    # Sobrescribe __str__ de la clase base (Person)
    def __str__(self):
        text = super(Worker, self).__str__()
        text += ", Salary {}".format(self.salary)
        return text

    def calc_yearly_salary(self):
        return self.salary * 12


# Crear una instancia de la clase Worker
worker_1 = Worker("Sparrow", 40, 176, 3000)

# Imprimir la representación en cadena y el salario anual
print(worker_1)
print(f'Yearly Salary: {worker_1.calc_yearly_salary()}')
```

Este código demuestra cómo se puede utilizar la herencia y la sobrecarga de métodos en Python para construir clases derivadas que extiendan el comportamiento de las clases base. La salida del código mostrará la información del trabajador, incluido su salario anual.

# Script operator_overloading.py explicado:

Este código define una clase llamada `Vector` que representa un vector bidimensional en términos de sus componentes `x` e `y`. La clase sobrecarga los operadores de suma (`__add__`) y resta (`__sub__`) para permitir la adición y sustracción de instancias de la clase `Vector`. Aquí está el código con explicaciones paso a paso:

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)

    def __str__(self):
        return "X: {}, Y: {}".format(self.x, self.y)

# Crear dos instancias de la clase Vector
vector_1 = Vector(2, 5)
vector_2 = Vector(6, 3)

# Imprimir las representaciones en cadena de los vectores
print(vector_1)
print(vector_2)

# Sumar dos vectores
vector_3 = vector_1 + vector_2
print(vector_3)

# Restar dos vectores
vector_4 = vector_1 - vector_2
print(vector_4)
```

Explicaciones:

- El método `__init__` es el constructor de la clase y se utiliza para inicializar las componentes `x` e `y` del vector.
  
- Los métodos `__add__` y `__sub__` sobrecargan los operadores de suma (`+`) y resta (`-`), respectivamente. Permiten sumar y restar instancias de la clase `Vector` creando un nuevo vector con las componentes resultantes.

- El método `__str__` proporciona una representación en cadena legible del vector cuando se utiliza la función `print()`.

- Se crean dos instancias de la clase `Vector` llamadas `vector_1` y `vector_2` con valores específicos para sus componentes `x` e `y`.

- Se imprimen las representaciones en cadena de `vector_1` y `vector_2`.

- Se realiza la suma (`vector_1 + vector_2`) y la resta (`vector_1 - vector_2`) de los vectores, creando nuevos vectores (`vector_3` y `vector_4`), respectivamente, y se imprimen los resultados.