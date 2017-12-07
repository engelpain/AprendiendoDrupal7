* Centro Nacional de Desarrollo e Investigación de Tecnologías Libres (CENDITEL)
* CENDITEL, Mérida - Venezuela
* Dirección de Desarrollo
* @author Ing. Angelo Osorio
* @date 2017-09-05 // (dd,mm,yyyy)
* Guía de hooks de Drupal 7.x

// Preámbulo [BEGIN] ---------------------------------------------------------------------------- //
Drupal es un CMS, creador bajo licencia GNU/GPL escrito en PHP.
La primera directiva de Drupal es Don't touch The Core, es decir, bajo ninguna circunstancia es
buena idea modificar los módulos que están dentro del core (/modules), para elaborar o incorporar
nuevos módulos se deben ingresar en la carpeta de módulos del sitio (/sites/all/modules).

Drupal funciona modularmente, por lo tanto de requiere algunos estádares para garantizar la
portabilidad de los módulos creados por la comunidad.

Un módulo (y los archivos que lo componen) llevarán siempre el nombre de la carpeta que lo contiene.
Por ejemplo: si un módulo se llama saludar, su carpeta contenedora se llamará saludar, también sus
archivos, por ejemplo: saludar.module, saludar.info, saludar.install

Esta guía está orientada a la creación de módulos de Drupal en su versión 7, para terminos práticos
se le llamará a este proyecto, modulo.

Nota: Los comentarios en drupal tiene el estándar de escribirse así:
/**
 * Comentarios
 * Más comentarios
 */
No significa que no se puedan usar comentarios como en PHP Nativo.

Menos en el .info, que los comentarios son así:
; Comentarios
; Más comentarios 

Terminada todas estas aclaratorias, se puede comenzar:
// Preámbulo [ENDED] ---------------------------------------------------------------------------- //



// Crear un módulo [BEGIN] ---------------------------------------------------------------------- //
La creación de módulos en drupal permite la expansión de las utilidades del CMS más allá de las que
trae por defecto.

Para crear un módulo (ultra sencillo y sin funcionalidades por ahora) en Drupal se pueden seguir los
siguientes pasos:

1. Utilizando la consola, acceso ftp o el manejador de archivos del que disponga, ir a la carpeta
del servidor donde tenga instalado drupal7, en mi caso, un servidor local Apache en Debian 9,
entonces se encuentra en la ruta /var/www/html, mi instalacion de drupal7 se encuentra en una
carpeta homónima, por lo tanto entraría en la carpeta /var/www/html/drupal7

2. Una vez dentro hay que entrar a la carpeta sites/all/modules

3. Dentro de modules hay que crear una carpeta a la que se llamará "modulo", luego de crearla,
entrar a ella.

4. Ahora hay que crear un archivo nuevo, que se llamará modulo.info (recordando que los archivos que
se encuentren dentro de la carpeta siempre son homónimos a ésta).

5. Utilizando el IDE de su preferencia (VIM, blog de notas, Sublime Text, Atom, etc...) hay que
escribir en el archivo modulo.info:

name = Modulo // El nombre del módulo, con este nombre se identificará de los demás módulos
description = Módulo de prueba que no hace nada // Breve descripción de lo que hará el módulo
package = Modulos de prueba // Declara a que paquete pertenece, puede 
dependencies[] = cck
dependencies[] = genpass
core = 7.x
version = "7.x-2.-dev"
project = "Planificación"









// Hooks [BEGIN] -------------------------------------------------------------------------------- //
- Los hooks son funciones creadas en php que realizan tareas ordenadas por el usuario dentro de
drupal.
// Hooks [ENDED] -------------------------------------------------------------------------------- //


/* --------------------------- hook_menu() [BEGIN] -------------------------- */
Define los items del menu y los callbacks de páginas.
Para crear un hook_menu() se reemplaza la palabra hook por el nombre del módulo,
por lo general los módulos tienen el mismo nombre de la carpeta que los contiene,
por lo tanto, 
Por ejemplo: function prueba_menu()

Dentro de los hooks hay items, que son palabras clave dentro de un arreglo
indexado por la ruta hacia donde apunta, se define con: $items[] = array();
Los items dentro del array se declaran de la siguiente forma:
function prueba_menu() {
    $items['abc/def'] = array(
        'item' => 'declaracion',
    );
    return $items;
}

Lista de items:
title:
Requerido. Título sin traducción del item.
Ejemplo: 'title' => 'Hello World',

title callback:
Función para generar el título; Por defecto a t(). Si sólo desea que se muestre
la cadena sin procesar, establezca esto en FALSE.
Ejemplo: 'title callback' => FALSE,

title arguments:
Argumentos enviados  a  t() o su  callback personalizado con la sustitucion del
path.

description:
La descripción sin traducción del item.
Ejemplo: 'description' => 'Ex ut nulla in.',

page callback:
Es la ruta hacia donde  apunta el  link  del menú,  también puede apuntar a
funciones.
Ejemplo: 'page callback' => 'hola_mundo',

page arguments:
Un array de  argumentos  para pasar a  la función page callback.

delivery callback:
La función para llamar al paquete del resultado de la función page callback y
enviarla al navegador.

access callback:
Una función que retorna TRUE si el usuario tiene derechos de acceso a este
elemento de menú y FALSE si no.
También puede ser una constante booleana en lugar de una función, y también
puede utilizar valores numéricos (se emitirá en booleano).
De forma predeterminada a user_access() a menos que se hereda un valor del
elemento de menú principal; sólo los elementos de MENU_DEFAULT_LOCAL_TASK pueden
heredar las devoluciones de llamada de acceso.
Para usar la devolución de llamada por defecto user_access(), debe especificar
el permiso para comprobar como "argumentos de acceso" (véase más abajo).
Ejemplo: 'access callback' => TRUE,
Ejemplo: 'access callback' => funcion_usuario,


access arguments: An array of arguments to pass to the access callback function,
with path component substitution as described above. If the access callback is
inherited (see above), the access arguments will be inherited with it, unless
overridden in the child menu item.

Un array de argumentos para pasar a la función access callback, con la
sustitución del componente de la ruta como se ha descrito anteriormente.
Si la devolución de llamada de acceso es heredado (ver arriba), los argumentos
de acceso serán heredados con él, a menos que anulado en el elemento de
menú hijo.




theme callback: (optional) A function returning the machine-readable name of the
theme that will be used to render the page. If not provided, the value will be
inherited from a parent menu item. If there is no theme callback, or if the
function does not return the name of a current active theme on the site, the
theme for this page will be determined by either hook_custom_theme() or the
default theme instead. As a general rule, the use of theme callback functions
should be limited to pages whose functionality is very closely tied to a
particular theme, since they can only be overridden by modules which
specifically target those pages in hook_menu_alter(). Modules implementing more
generic theme switching functionality (for example, a module which allows the
theme to be set dynamically based on the current user's role) should use
hook_custom_theme() instead.

theme arguments: An array of arguments to pass to the theme callback function,
with path component substitution as described above.

file: A file that will be included before the page callback is called; this
allows page callback functions to be in separate files. The file should be
relative to the implementing module's directory unless otherwise specified by
the "file path" option. Does not apply to other callbacks (only page callback).

file path: The path to the directory containing the file specified in "file".
This defaults to the path to the module implementing the hook.

load arguments: An array of arguments to be passed to each of the wildcard
object loaders in the path, after the path argument itself. For example, if a
module registers path node/%node/revisions/%/view with load arguments set to
array(3), the '%node' in the path indicates that the loader function node_load()
will be called with the second path component as the first argument. The 3 in
the load arguments indicates that the fourth path component will also be passed
to node_load() (numbering of path components starts at zero). So, if path
node/12/revisions/29/view is requested, node_load(12, 29) will be called. There
are also two "magic" values that can be used in load arguments. "%index"
indicates the index of the wildcard path component. "%map" indicates the path
components as an array. For example, if a module registers for several paths of
the form 'user/%user_category/edit/*', all of them can use the same load
function user_category_load(), by setting the load arguments to
array('%map', '%index'). For instance, if the user is editing category 'foo' by
requesting path 'user/32/edit/foo', the load function user_category_load() will
be called with 32 as its first argument, the array ('user', 32, 'edit', 'foo')
as the map argument, and 1 as the index argument (because %user_category is the
second path component and numbering starts at zero). user_category_load() can
then use these values to extract the information that 'foo' is the category
being requested.

weight: Un integer que determina la posición relativa de los items en el menú.
------- Por defecto es 0.
------- Los items del men{u con el mismo peso son ordenados alfabeticamente.


menu_name: Optional. Set this to a custom menu if you don't want your item to be
placed in Navigation.

expanded: Optional. If set to TRUE, and if a menu link is provided for this menu
item (as a result of other properties), then the menu link is always expanded,
equivalent to its 'always expanded' checkbox being set in the UI.

context:
(optional) Defines the context a tab may appear in. By default, all tabs are
only displayed as local tasks when being rendered in a page context.
All tabs that should be accessible as contextual links in page region containers
outside of the parent menu item's primary page context should be registered
using one of the following contexts:
    MENU_CONTEXT_PAGE: (default) The tab is displayed as local task for the page
    context only.
    MENU_CONTEXT_INLINE: The tab is displayed as contextual link outside of the
    primary page context only.
Contexts can be combined. For example, to display a tab both on a page and
inline, a menu router item may specify:
'context' => MENU_CONTEXT_PAGE | MENU_CONTEXT_INLINE,

tab_parent:
For local task menu items, the path of the task's parent item; defaults to the
same path without the last component (e.g., the default parent for
'admin/people/create' is 'admin/people')

tab_root:
For local task menu items, the path of the closest non-tab item; same default as
"tab_parent"

position:
Position of the block ('left' or 'right') on the system administration page for
this item.

type:
A bitmask of flags describing properties of the menu item. Many shortcut
bitmasks are provided as constants in menu.inc:
    MENU_NORMAL_ITEM: Normal menu items show up in the menu tree and can be
    moved/hidden by the administrator.
    MENU_CALLBACK: Callbacks simply register a path so that the correct
    information is generated when the path is accessed.
    MENU_SUGGESTED_ITEM: Modules may "suggest" menu items that the administrator
    may enable.
    MENU_LOCAL_ACTION: Local actions are menu items that describe actions on the
    parent item such as adding a new user or block, and are rendered in the
    action-links list in your theme.
    MENU_LOCAL_TASK: Local tasks are menu items that describe different displays
    of data, and are generally rendered as tabs.
    MENU_DEFAULT_LOCAL_TASK: Every set of local tasks should provide one
    "default" task, which should display the same page as the parent item.
If the "type" element is omitted, MENU_NORMAL_ITEM is assumed.

options:
An array of options to be passed to l() when generating a link from this menu
item. Note that the "options" parameter has no effect on MENU_LOCAL_TASK,
MENU_DEFAULT_LOCAL_TASK, and MENU_LOCAL_ACTION items.

Información extraída desde:
https://api.drupal.org/api/drupal/modules!system!system.api.php/function/hook_menu/7.x
/* --------------------------- hook_menu() [ENDED] -------------------------- */