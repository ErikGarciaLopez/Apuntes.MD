# Kotlin 1

## Crear vista
package > New > Activity > Empty Views Activity

## Poner vista como punto de entrada
manifests > AndroidManifests.xml

En el `<activity>` que deseemos ponemos `<intent-filter>`

Ejemplo:
```xml
<activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
```

Se pueden tener 2 intent-filter y se crean 2 aplicaciones

## Agregar elemento a la interfaz
En el layout hay elementos como TextView, Button, imageView, etc.

* Arrastramos el elemento
* Poner constraints al elemento (ligar los 4 puntitos del elemento a la pantalla)
* Podemos modificar los atributos para cambiar el texto (text), tamaño(textSize) , mover posicion, padding, margin, 

## Usar clip arts

res > drawable > new > Vector Asset y añadimos el clip art

En el imageView en la propiedad srcCompat > Pick a Resource y lo seleccionamos

## Agregar imagen

La agregamos en drawable

Si la queremos usar de background:
```kotlin
android:background="@drawable/nombreimagen"
```
O bien, en el atributo background

A las imagenes JPG les podemos dar clic derecho > Convert to WebP y pesa menos

## Interactuar con un elemento de la interfaz desde Kotlin

El elemento en sus atributos tiene un id, desde el codigo nos vamos a referir a el por su id.
El prefijo es el tipo de elemento del que se trata. Ej:

* textView -> tvSaludo
* button -> btnSaludo


### Habilitar bindings (viewbinding)
En build.gradle.kts (Module :app)
```kotlin
buildFeatures {
        viewBinding = true
    }
```
Sincronizamos el gradle

### Referenciar MainActivity

En el Activity.kt ponemos el `lateinit` como `binding`, la inflamos y la establecemos como vista
```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding //lateinit
    override fun onCreate(savedInstanceState: Bundle?) {

        binding = ActivityMain2Binding.inflate(layoutInflater) //Inflamos
        setContentView(binding.root) //Con root
    }

}
```
### Usar las variables
Hecho lo anterior podemos usarlas:

```kotlin
binding.tv.text = "0"
```

### Interactuar al dar clic

Utilizamos el metodo `setOnClickListener` con la lambda (el que dice -> Unit)

```kotlin
binding.btnOk.setOnClickListener {
    //Click del boton
    val numero = binding.etNumero.text.toString() //Ej leer texto de un edit text
    binding.tvResultado.text = "El numero que ingresaste es $numero" // Ej mostrar variable en text
}
```

### Transicionar a otra pantalla
Se usan los `Intent()`, recibe de parametro el contexto y la clase del activity que quiero abrir
```kotlin
binding.btnOk.setOnClickListener {
    val intent = Intent(this, MainActivity2::class.java)
    startActivity(intent)
}
```
Se maneja el backStack y almacena como se va navegando y podemos regresar utilizando la flecha

### Pasar variables a otra Activity

Generamos un objeto (params) de la clase Bundle

Al tener la variable params ya podemos utilizar los metodos para pasar informacion (put), se pasan con llave-valor.

Al intent con `putExtras` le pasamos el Bundle

```kotlin
binding.btnOk.setOnClickListener {

    val params = Bundle() //Bundle
    params.putInt("age", 25) //Int
    params.putString("name", "Elena") //String
    params.putBoolean("loyalty", false) //Boolean

    val intent = Intent(this, MainActivity2::class.java)

    intent.putExtras(params) //Mandamos el Bundle

    startActivity(intent) 
}
```

Tambien se puede con `bundleOf()` que hace inferencia de datos:
```kotlin
binding.btnOk.setOnClickListener {

    val params = bundleOf(
        "age" to 25,
        "name" to "Elena",
        "loyalty" to false
    )   //Con bundleOf

    val intent = Intent(this, MainActivity2::class.java)
    intent.putExtras(params) //Mandamos el Bundle
    startActivity(intent)  
}
```

### Recuperar el bundle en otra Activity
Recuperamos el bundle (las variables) con intent.extras

Lo hacemos con `?` por si en null

El `let` nos da los argumentos en la variable de la lambda (si no le ponemos nombre es con it). Con el setter accedemos utilizando la llave y defaultValue
```kotlin
val params = intent.extras

params?.let {
val name = it.getString("name", "")
val age = it.getInt("age", 0)

}
```

Se recomienda no usar el it:
```kotlin
val params = intent.extras

params?.let { args ->
val name = args.getString("name", "")
val age = args.getInt("age", 0)

}
```

## Mensajes Toast
Son mensajes que no tienen interaccion y desaparecen

Pide como argumentos el contexto, el texto y la duracion que puede ser LENGTH_SHORT o LENGTH_LONG, lo mostramos con un `show()`
```kotlin
Toast.makeText(
    this,
    "Nombre recibido: $name, edad: $age",
    Toast.LENGTH_SHORT
).show()
```

## Poner fuente
 A la izquierda en las figuras geometricas (resource manager) > tres puntos > Font > + > More Fonts > Elegimos una o subimos un .ttf > Puede ser en "Create downloadable font" 

 Para usarla: drawable > new > Android resoruce directory > resource type: Font

 Ahi pegamos el ttf

 Para usarla en nuestro elemento text es en el atributo `fontFamily`


## Debuggear

### Con println
No es lo ideal. Abrimos el Logcat y podemos filtrar:
```
package:mine System.out
```

### Con Log
d debug, e error, i info

Log.d("APPSLOG", "El valor de a es: $a")

Filtramos por la etiqueta que es APPSLOG

La etiqueta se puede poner en un Constants.file
```kotlin
object Constants{
    const val LOGTAG = "APPLOG"
}
```

Y ya se usaria asi:
```kotlin
Log.d(Constants.LOGTAG, "El valor de a es: $a")
```

### Con Breakpoints

Con breakpoints y en la catarina

## Usar colores

En res > values > colors.xml podemos agregar colores
```xml
<color name="my_blue">#2196F3</color>
```
Le podemos poner #FF para el canal alpha

En el codigo usamos el color asi (sin hardcodear):
```kotlin
android:background="@color/my_blue"
```

Tambien se puede crear primero el color:  @color/my_red y como no existe aun el IDE nos deja crearlo

## Usar strings sin hardcoding
En res > values > strings.xml ponemos las cadenas desde xml o en "Open editor"

```xml
<string name="Greeting">Hola cómputo móvil</string>
```

Asi se usa desde el codigo:
```kotlin
android:text="@string/Greeting"
```

Igual se puede crear el "@string/Greeting" primero y despues desde el IDE lo creamos