# Taller GameVotes

## Enunciado

Un club universitario de desarrollo y crítica de videojuegos necesita una aplicación para administrar su catálogo de juegos independientes (*indie*).
Los miembros podrán registrar videojuegos, localizar los que les interesan, borrar videojuegos, editar sus datos y expresar su apoyo mediante un botón «Votar».
El club desea consultar un ranking de popularidad.

Creen un nuevo proyecto. Utilicen **ArrayList, búsqueda lineal, búsqueda binaria, ordenamiento y Java Swing**.
La lógica debe quedar separada de los eventos de la interfaz.

El equipo trabajará en **un único repositorio de GitHub**, con commits de código desde **al menos tres cuentas distintas**. 
Cada integrante debe realizar al menos un commit significativo.

## Datos del videojuego

| Atributo | Tipo | Regla |
|---|---|---|
| `codigoID` | `int` | Positivo, único después del registro. |
| `nombre` | `String` | Obligatorio; puede repetirse en videojuegos con códigos diferentes. |
| `estudio` | `String` | Obligatorio; puede repetirse (estudio o desarrollador). |
| `categoria` | `String` | Obligatorio; seleccionado de un JComboBox. |
| `anioLanzamiento` | `int` | Desde 1980 hasta el año actual. |
| `votos` | `int` | No negativo; inicialmente 20 para videojuegos nuevos. Solo disminuye mediante el botón Votar. |

Las categorías del ejercicio son Acción, Estrategia, RPG, Plataformas y Simulación.

## Organización de los datos

La colección principal será `ArrayList<Videojuego>`. Cree un método para que se encuentre ordenada por código de manera descendente para utilizar la búsqueda binaria.

Para el ranking, muestre los datos ordenados por votos de manera descendente.
La lista principal debe conservar su orden para que sigan funcionando nuevos ingresos y búsquedas.

## Requerimientos funcionales

### R1 Cargar veinte videojuegos al iniciar

- En un primer Tab de un componente `JTabbedPane`, listar todos los elementos en un `JList`.
- Precargar exactamente veinte videojuegos.
- Revisar que no se ingresen códigos duplicados y que se permitan valores repetidos en categoría, año de lanzamiento y votos.
- Cargar una sola vez durante la ejecución. Cambiar de pestaña, buscar o actualizar el ranking no debe reiniciar los contadores ni duplicar registros.
- Mostrar la cantidad actual de videojuegos. Trabajar en memoria; no se exige persistencia en archivos ni base de datos.

### R2 Registrar nuevos videojuegos

- En el primer Tab del `JTabbedPane`, crear los controles para registrar nuevos videojuegos.
- Incorporar un formulario de ingreso con código, nombre, estudio, categoría y año de lanzamiento, más el botón **Registrar**.
- Validar los campos obligatorios, el código positivo, el año permitido y que no exista otro registro con el mismo código.
- Los nuevos videojuegos comienzan con cero votos; ese valor no se escribe en el formulario.
- Si hay errores, mostrar un mensaje sin registrar parcialmente el videojuego ni cambiar los datos anteriores.

Debe poder registrarse un código menor que los existentes, por ejemplo `1050`. No se puede asumir que los nuevos códigos siempre pertenecen al final de la lista ordenada.

### R3 Buscar coincidencias de texto

- En un segundo Tab del componente `JTabbedPane`, implementar búsqueda lineal sobre nombre y estudio únicamente por exactitud:
- Mayúsculas y minúsculas serán diferentes (*case-sensitive*).
- Incluir un videojuego si el texto exacto aparece en el nombre **o** en el nombre del estudio, haciéndolo desde un solo `JTextField` y un solo botón.
- Rechazar consultas nulas, vacías o formadas solo por espacios.
- Mostrar los resultados en un `JTextArea`.

### R4 Buscar por código

- En el segundo Tab, implementar una búsqueda binaria propia sobre la colección principal:
- Devolver el índice correspondiente o `-1` cuando no exista.
- Rechazar códigos no positivos.
- Al encontrar un videojuego, cargar sus datos en componentes para la edición o mostrar un mensaje de que no existe el elemento buscado.
- Permitir modificar nombre, estudio, categoría y año de lanzamiento. No editar código ni escribir manualmente el contador de votos.
- Validar todos los nuevos valores antes de guardar. Si uno falla, no modificar parcialmente los otros atributos.
- Si el código no se encuentra, mostrar un aviso y limpiar cualquier selección anterior para evitar cambios sobre otro videojuego.
- Al actualizar los datos, mostrar un aviso mediante `showMessageDialog`; estos cambios deben reflejarse en el Tab 1 en el listado de videojuegos.
- Agregar un botón Borrar: una vez buscado por código y encontrado el videojuego, habilitar o usar un botón para **ELIMINAR VIDEOJUEGO**, que lo elimina del `ArrayList` por completo.

### R5 Votar por un videojuego seleccionado

- En el segundo Tab:
- Buscar por código y, una vez encontrado el videojuego, disponer de un spinner con valores de 1 a 3 botón para pulsar **Restar Votos**.
- Cada clic válido decrementa el contador del registro seleccionado segun el valor del spinner.
- Mostrar el contador actualizado y refrescar las vistas correspondientes.
- Sin una selección válida, mostrar un aviso sin modificar ningún videojuego.
- Para esta simulación se permiten varios clics sobre el mismo videojuego. No se requieren cuentas de usuarios ni la operación de quitar voto.

El incremento ocurre únicamente al pulsar el botón.

### R6 Ordenar el ranking

Implementar el siguiente método:
- En el tercer Tab:
- Mostrar en un nuevo `JList` todos los elementos ordenados por cantidad de votos de forma descendente.
- Conservar todos los videojuegos, incluso cuando tengan la misma cantidad de votos.
- Mostrar en el `JList` el código, nombre y contador de votos de cada videojuego.
- Después de consultar el ranking, la búsqueda binaria por código debe seguir funcionando correctamente.

## Interfaz requerida con JTabbedPane

La interfaz debe ser elaborada manualmente por los estudiantes.
Después de registrar, editar, eliminar o votar, actualizar las vistas afectadas sin volver a cargar los datos iniciales. Si una edición hace que el videojuego deje de coincidir con el texto buscado, recalcular los resultados y limpiar la selección cuando corresponda.

## Trabajo en GitHub y entrega

1. Crear un repositorio único por equipo, accesible al docente.
2. Incluir commits de código desde al menos tres cuentas diferentes y al menos un aporte significativo por integrante.
3. No se exige utilizar ramas ni pull requests. Pueden trabajar con el procedimiento de carga que aprendieron en clase, conservando la autoría de cada aporte.
4. Entregar enlace al repositorio, código integrado, capturas de las tres pestañas y evidencia de los casos de comprobación.
5. Completar la tabla de aportes. Cualquier integrante debe poder ejecutar el programa y explicar la colaboración del equipo.

| Integrante | Usuario GitHub | Mensaje de commit |
|---|---|---|
| | | |

Verificar que GitHub muestre correctamente la autoría. Si utilizan Git local, configurar un correo asociado a la cuenta correspondiente. No compartir cuentas.

## Rúbrica sobre 10 puntos

| Criterio | Puntaje máximo | Evidencia |
|---|---|---|
| Funcionamiento | 3 | Los seis requerimientos y los casos de comprobación funcionan. Cualquier integrante ejecuta la demostración. |
| Interfaz realizada manualmente por los estudiantes | 4 | JTabbedPane, formularios, JList, botones y mensajes conectados correctamente. Cualquier integrante ejecuta y muestra la interfaz. |
| GitHub | 3 | Un repositorio, commits desde al menos tres cuentas y aportes identificables. |
