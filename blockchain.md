Blockchain



El Blockchain es una cadena de bloques con mucha similitud a una estructura de datos denominada Linked List o Lista Enlazada. Cada bloque esta conectado a otro bloque en la cadena y contiene información sobre una transacción en particular, una marca de tiempo, y un hash criptográfico del bloque previo.

Nuestro blockchain utilizará como mínimo lo:

* el hash [SHA-256](https://en.wikipedia.org/wiki/SHA-2), ver: [Hashlib](https://docs.python.org/3.5/library/hashlib.html?highlight=hashlib%20sha256)
* [Greenwich Mean Time](https://en.wikipedia.org/wiki/Greenwich_Mean_Time), ver: [Datetime](https://docs.python.org/3.5/library/datetime.html)
* String como tipaje de datos para la informacion, ver: [Str](https://docs.python.org/3.5/library/stdtypes.html#text-sequence-type-str)



La idea es que un bloque debería contener lo siguiente.

![image-20191213232613423](/home/adriaanbd/.config/Typora/typora-user-images/image-20191213232613423.png)



Para programar el concepto de un Blockchain necesitamos tres cosas:

* Una clase denominada Bloque
* Un metodo para obtener el hash de la información del bloque
* Una clase denominada Cadena



El Bloque podrá ser algo asi:

```python
import hashlib

class Bloque:

    def __init__(self, timestamp, data, previous_hash):
      self.timestamp = timestamp
      self.data = data
      self.previous_hash = previous_hash
      self.hash = self.calc_hash()
    
    def calc_hash(self):
      sha = hashlib.sha256()

      hash_str = "We are going to encode this string of data!".encode('utf-8')

      sha.update(hash_str)

      return sha.hexdigest()
```



La Cadena (repasar el concepto de LinkedList de ser necesario):

```python
class Cadena:
	def __init__(self, #argumentos):
        """Variables necesarios para por lo menos identificar el primer bloque y/o el último bloque"""
    def agregar_bloque(self):
        """Agrega un bloque a la cadena. El primer bloque es especial."""
    def verificar_integridad(self):
        """Revisa la integridad de la cadena, bloque por bloque, asegurandose previous_hash sea igual al hash del bloque previo [OPCIONAL]"""
    def crear_fork(self):
    	"""Copia la cadena entera o un segmento de ella desde un punto en adelante [OPCIONAL]"""
```



Adicionalmente, pensar en casos especiales como:

* Crear un bloque con otro tipo de data como `None`, `int`, etc. debería indicar que solo aceptan data tipo `str`.
* Crear un bloque con un empty `str`, i.e. `""` debería indicar que no se puede crear un bloque sin data.
