<h1>Crear módulos en Drupal 7</h1>
<p> Centro Nacional de Desarrollo e Investigación de Tecnologías Libres (CENDITEL)</p>
<p> <a href="https://www.cenditel.gob.ve/">CENDITEL</a>, Mérida - Venezuela </p>
<p> Dirección de Desarrollo </p>
<p> Autor: <a href="https://twitter.com/Engel_PAIN">Ing. Angelo Osorio</a> </p>
<p> Fecha de Elaboración: 14-12-2017 (dd,mm,aaaa)</p><br>

<h2>Nota del autor</h2>
<p> En drupal las rutas de los directorios se escriben obviando el nombre que poseé el sitio, si por
ejemplo, el core de drupal está en un directorio que se llame "ejemplo", para relatar donde se
encuentra algo dentro de ese directorio, no se escribe <code>ejemplo/ruta/relatada</code> sino que
se obvia el nombre del directorio, por ejemplo, la ruta anterior se escribiría:
<code> ruta/relatada </code>
</p>
<p> Terminada esta aclaratoria se puede comenzar a desarrollar. </p>

<h2>¿Dónde van los módulos?</h2>
<p> Los módulos de terceros elaborados para <strong> Drupal 7 </strong> no van en
<code> modules </code> (el primer directorio con ese nombre dentro del core) como sería de esperarse
a primera vista, sino van en <code> sites/all/modules </code> y es porque en la primera van sólo los
módulos que hacen funcionar el core, por eso no es recomendable bajo ninguna circunstancia, guardar
los módulos de terceros allí.
</p>


<h2> Archivos del módulo </h2>
<p> Para crear un módulo, primero hay que crear el directorio que lo contandrá, por lo general los
archivos de los módulos son homónimos al nombre del directorio que los contiene.
</p>
<p> Para este ejemplo se creará un directorio llamado <code> saludo </code> </p>
<p> Dentro del directorio se deben crear 2 archivos: saludo.info y saludo.module </p>

<h3> saludo.info </h3>
<p> Éste archivo indica informaciones sobre el módulo: nombre, descripción breve de para que sirve,
el paquete al que pertenece, con que versión de drupal será compatible, las dependencias del módulo,
cuando fue creado, y otros atributos que son opcionales.
</p>
<p> <b> Nota: </b> Los comentarios en los archivos .info son de una sola línea y se abren con un
punto y coma (<b> ; </b>), por ejemplo:</p>
<p>
  <code> ;Esto es un comentario</code>
</p>

<h4> Código dentro de saludo.info </h4>
<p>
  <code>
    ;name: se utiliza para declarar el nombre del módulo que se está creando. <br>
    name = Saludo
  </code> <br>
  <code>
    ;description: Se utiliza para declarar una pequeña descripción de la utilidad del módulo. <br>
    description = "Módulo para saludar al usuario hola mundo"
  </code> <br>
  <code>
    ;package: Se utiliza para declarar a que paquete pertenece el módulo, se puede <br>
    ;dejar vacío este campo, escribir el nombre de paquetes ya existentes como tools <br>
    ;o crear nuevos paquetes como en este caso. <br>
    package = Aprendiendo Drupal
  </code> <br>
  <code>
    ;core: Declara el núcleo de drupal con el que será compatible. <br>
    core = 7.x
  </code>
</p>