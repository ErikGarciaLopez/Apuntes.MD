# DataStructures Java

## LinkedList vs ArrayList

Tienen los mismos metodos (pues ambos implementan la interfaz List), solo cambia la forma en que se maneja detras de escenas. Cada una tiene sus propias características y rendimiento.

### LinkedList
```java
LinkedList<String> namesLinkedList = new LinkedList<>();
namesLinkedList.add("John");
namesLinkedList.add("George");

namesLinkedList.get(1);

namesLinkedList.add(1,"George");
```

* Para encontrar un elemento con .get() tiene que recorrer las posiciones anteriores a el para encontrarlo
* Es eficiente para añadir o remover elementos, pues solo cambia los apuntadores


### ArrayList
```java
ArrayList<String> namesArrayList = new ArrayList<>();
namesArrayList.add("John");
namesArrayList.add("George");

namesArrayList.get(1);

namesArrayList.add(1,"George");
```

* Para encontrar un elemento con .get() lo encuentra inmediatamente O(1)
* Para añadir o remover elementos tiene que crear todo un nuevo arreglo, por lo que es tardado

### Metodos

* `add(E e)`: Añade un elemento al final de la lista.
add(int index, E element): Añade un elemento en una posición específica.
* `remove(int index)`: Elimina el elemento en la posición especificada.
* `remove(Object o)`: Elimina la primera aparición de un objeto específico.
* `get(int index)`: Devuelve el elemento en la posición especificada.
* `set(int index, E element)`: Reemplaza el elemento en la posición especificada.
* `size()`: Devuelve el número de elementos en la lista.
* `clear()`: Elimina todos los elementos de la lista.
contains(Object o): Devuelve true si la lista contiene el elemento especificado.
* `isEmpty()`: Devuelve true si la lista no contiene ningún elemento.
* `indexOf(Object o)`: Devuelve la posición del primer elemento igual al especificado.
* `lastIndexOf(Object o)`: Devuelve la posición del último elemento igual al especificado.
* `toArray()`: Convierte la lista en un arreglo de objetos.
subList(int fromIndex, int toIndex): Devuelve una vista de la porción especificada de la lista.


## HashSet

```java
Set<String> names = new HashSet<>();

names.add("Walter");
names.remove("Walter");
names.contains("Walter");
names.clear();

//Iterar con enhanced loop
for (String name: names){
    System.out.println(name);
}

//Iterar con for each
names.forEach(System.out::println);

//Iterar con iterador
Iterator<String> namesIterator = names.iterator();
while (namesIterator.hasNext()){
    System.out.println(namesIterator.next());
}
```

* No mantiene ningún orden.
* No permite duplicados.
* No se puede eliminar por indice, ya que no hay orden.

### Ejemplo: Eliminar duplicados de una lista

```java

List<Integer> numberList = new ArrayList<>();
numberList.add(1);
numberList.add(2);
numberList.add(3);
numberList.add(2);
numberList.add(1); 
System.out.println(numberList); // [1, 2, 3, 2, 1]

Set <Integer> numberSet = new HashSet<>();
numberSet.addAll(numberList);
System.out.println(numberSet); //[1, 2, 3]

```

## TreeSet
```java
Set<String> names = new TreeSet<>();
```
Funciona igual que el HashSet pero si mantiene un orden (no en orden de insercion pero si un orden natural, ej. alfabetico).

Sin embargo el HashSet es mucho mas rapido que el TreeSet.

## LinkedHashSet
```java
Set<String> names = new LinkedHashSet<>();
```
Funciona igual que el HashSet pero si mantiene un orden (no natural, sino de insercion).

No es tan rapido como el HashSet, pero es mucho mas rapido que el TreeSet.


## HashMap

Es una estructura de datos que almacena pares clave-valor.

```java
HashMap<String, Integer> empIds = new HashMap<>();

empIds.put("John", 12345);
empIds.put("Carl", 54321);
empIds.put("Jerry", 8675309);

System.out.println(empIds); //{Carl=54321, John=12345, Jerry=8675309}

System.out.println(empIds.get("Carl")); //54321

System.out.println(empIds.containsKey("Jerry")); //True

System.out.println(empIds.containsValue(6)); //False

empIds.replace("John", 777); //{John = 777}

empIds.putIfAbsent("John", 222); //No lo pone porque John ya existe
empIds.putIfAbsent("Steve", 222); //Si lo pone

empIds.remove("Steve");



```

* No garantiza un orden en especifico
* Se actualiza el valor si se inserta una llave que ya existia 


