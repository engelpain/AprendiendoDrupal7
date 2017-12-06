<h1> Guía de instalación de Drupal 7.x </h1>
<p> Centro Nacional de Desarrollo e Investigación de Tecnologías Libres (CENDITEL)</p>
<p> CENDITEL, Mérida - Venezuela </p>
<p> Dirección de Desarrollo </p>
<p> Autor: <a href="https://twitter.com/Engel_PAIN">Ing. Angelo Osorio</a> </p>
<p> Fecha de Elaboración: 01-09-2017 (dd,mm,aaaa)</p><br>

<h2>Notas del Autor</h2>
<p> Drupal es un CMS creado bajo licencia GNU/GPL escrito en PHP, lo que lo hace portable para cualquier sistema operativo (sea Linux, Windows o Mac) que disponga de un navegador web, y requiere PHP, un Servidor local y MariaDB/MySQL o PostgreSQL para su instalación.</p>
<p><b>Importante:</b> Dado que esta instalación se realizó en Debian 9, se harán muchos de los pasos desde la consola (Like a Boss). No significa que no se pueda realizar sin la consola, también se puede realizar desde el gestor de archivos de su preferencia.</p>
<p>El símbolo al principio de una línea de comandos indica: <br>
  <code>  $ = hacer la sentencia como usuario </code> <br>
  <code>  # = hacer la sentencia como administrador</code>
</p>

<h3>Requisitos previos para la instalación de Drupal 7.x</h3>
<ul>
  <li> Apache, nginx o cualquier servidor que admita PHP </li>
  <li> Php5.3 o superior, Php7 </li>
  <li> MariaDB/MySQL o PostgreSQL </li>
  <li> Navegador Web</li>
</ul>

<h3>Equipo del tutorial:</h3>
<ul>
  <li> Debian 9.2 Stretch </li>
  <li> PHP 7.0.19-1 </li>
  <li> Postgresql 9.6.4 </li>
  <li> Apache 2.4.25 </li>
</ul>

<h2> Instalacion Drupal 7.x </h2>
<ul>
  <li>
    <p> Para realizar la instalación de Drupal primero hay que descargar su núcleo desde el navegador, desde su <a href="https://ftp.drupal.org/files/projects/drupal-7.56.zip"> página oficial</a> para obtener la versión más actualizada de Drupal 7 (Enlace obtenido el 01-09-2017).
    </p>
  </li>
  <li>
    <p>
      Luego de descargar el núcleo hay de descomprimir el archivo que anteriormente se descargó en el directorio del servidor, en este caso la carpeta <code>var/www/html</code>
    </p>
  </li>
  <li>
    <p>
      Se le puede dar un nombre arbitrario a la carpeta que se descomprimió, para este ejemplo se le llamará <strong>drupal7</strong> al directorio para mayor comprensión de la información.
    </p>
  </li>
  <li>
    <p>
      Desde la consola se entrará a la carpeta sites/default dentro del sistema usando en comando:
    </p>
    <p>
      <code>  $ cd /var/www/html/drupal7/sites/default</code>
    </p>
  </li>

6. Hay que realizar una copia del archivo default.settings.php con el nombre settings.php que será
el que guarde todos los datos de configuración de Drupal
$ cp default.settings.php settings.php

7. Ahora hay que cambiarle los permisos de configuración al archivo (como root)
$ su
# chmod 777 settings.php

8. Dentro de la misma carpeta se debe crear los directorios files, themes y modules para el correcto
comportamiento de Drupal en la posterior instalación:
# mkdir files
# mkdir themes
# mkdir modules

9. Salimos de la carpeta default
# cd ..

10. Entramos en el directorio all y creamos también los directorios files, themes y modules para el
correcto comportamiento de Drupal en la posterior instalación:
# cd all
# mkdir files
# mkdir themes
# mkdir modules

Nota: Drupal trabaja bajo la directiva DTC, significa: Don't Touch the Core Drupal posee directorios
donde se deben ingresar los módulos externos y los temas, sin embargo, los directorios donde se
deben ingresar no son los primeros que se encuentran al abrir la carpeta de Drupal, sino los que hay
dentro de sites/all/

11. Ahora se debe crear una base de datos en PostgreSQL o MySQL, con un nombre cualquiera, para este
ejemplo se utilizará el nombre de drupal7.

12. Desde un navegador web se debe ingresar al directorio que se creó en el paso 2 escribiendo en la
barra de URL localhost/drupal7 Automáticamente comenzará la instalación de Drupal 7.
</ul>