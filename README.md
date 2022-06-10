# RPG-Unity
Repositorio del proyecto del curso de Diseño avanzado de RPG con Unity.

Importante: El contenido de este curso es propiedad de su creador Juan Diego Vásquez Moreno, el propósito de este repositorio es documentar mi proceso para fines de aprendizaje.

## Preparación del proyecto

- Al iniciar un proyecto nuevo es importante cambiar el dispositivo al cual va a estar dirigido nuestro juego para que se pueda testear de forma apropiada.

- Si no deseamos que nuestro juego tenga la opción de girar la pantalla deshabilitamos esta opción yendo a Edit -> Project Settings -> Player. En el campo resolution and presentation.

- Es importante desde el inicio establecer medidas estándar para que los Pixels per unit en nuestro proyecto sean coherentes.

### Creación de presets para configurar assets
En caso de trabajar con grandes volúmenes de sprites o assets, será difícil configurar todos de forma manual, por lo tanto podemos crear presets que los configuren automáticamente, para ello hacemos lo siguiente:

1. Seleccionamos el asset que necesitamos o queremos tomar como referencia.
2. En la ventana inspector seleccionamos el ícono que asemeja unos sliders y nos desplegará los presets existentes.
3. Damos click en el botón `Save content to`
4. Lo nombramos y seleccionamos la carpeta donde queremos que se guarde
5. Al guardarlo se genera un nuevo archivo con la configuración, si seleccionamos este archivo, en el inspector veremos el botón `Add to Texture Importer default`, hacemos click en él y ahora cada vez que importes un nuevo sprite se va a configurar de esta manera.




## Creación de escenarios

Para este paso es importante realizar una correcta configuración de los Assets con los cuales vamos a trabajar, para este curso se han recomendado el uso de los siguientes packs de assets:

- [Generic RPG pack de Estúdio Vaca Roxa](https://bakudas.itch.io/generic-rpg-pack)
- [RPG asset tileset interior pack de Gif](https://gif-superretroworld.itch.io/interior-pack)

Como estamos trabajando con pixel art no debemos usar compresión y el filter mode debe estar configurado como Point(no filter). En caso de trabajar con un atlas o con una animation sheet, el sprite mode debe configurarse como multiple para poder cortarse con el sprite editor.

Para poder pintar el escenario de forma sencilla, debemos preparar las diferentes "capas" o tilemapsque va a tener, en el caso de este proyecto se usan las siguientes:

| Tilemap | Mode | Sorting Layer | Order in Layer|
| ------------- |:-------------:| -----:| -----:|
|`Ground`|Chunk|Background|0|
|`Ground decorations`|Chunk|Background|1|
|`Walkable`|Individual|Default|0|
|`Foreground`|Chunk|Foreground|0|
|`Collision`|Chunk|Foreground|0|

Ahora sí podemos comenzar a pintar nuestro escenario respetando siempre el Tilemap en donde se quiere pintar, de lo contrario nuestros objetos pueden mostrarse de forma incorrecta.

Si tenemos dos objetos en la misma Sorting Layer y con el mismo Order in Layer, se mostrará por encima de acuerdo al sort order y al pivote. Para arreglar esto, vamos al menú Edit -> Project Settings -> Graphics, en el apartado de Camera Settings tenemos el apartado `Transparency Sort Mode`, aquí seteamos como Custom Axis, esto significa que los sprites se ordenarán según uno de los ejes que le indiquemos, en este caso vamos a indicar que queremos ordenar de acuerdo al eje Y. La razón es muy sencilla, si el personaje se mueve hacia arriba en el eje Y lo que queremos es que parezca que se mueve detras del objeto, de manera que el sprite del objeto en cuestión, se posicionara delante. Esto va a crear la ilusión de que nos movemos delante y detrás de los objetos dentro de una misma sorting layer.



![Touch_RPG - SampleScene - iOS - Unity 2020 3 2f1_ _DX11_ 2022-06-10 14-01-16](https://user-images.githubusercontent.com/81669610/173134302-4e737f0f-0d8d-4032-aae5-804911a0a3d6.gif)


Para que lo anterior funcione correctamente, debemos asegurarnos de que:
1. Los sprites de los game objects que van a interactuar tengan configurado el pivote a partir de donde queremos que se ordene, es decir hasta abajo de la imagen en este caso. Para hacer esto, seleccionamos el sprite y en el inspector buscamos el apartado `Pivot` y lo podemos configurar como bottom o custom. Una forma difetente de hacerlo es entrar al sprite editor y configurarlo manualmente desde ahí.
2. Si el sprite es parte de una Tile Palette, es decir, se va a renderizar en un Tilemap, es importante configurar el eje del anchor en el apartado `Tile Anchor` del componente Tilemap en Y a para que no "suba" el sprite en el tilemap.


